# Caso 03 — Expansión LATAM: "DocuSign-AR"

> Caso ficticio. Empresa, nombre y datos inventados. DocuSign es una marca registrada de
> DocuSign Inc.; el nombre se usa solo como referencia descriptiva del tipo de producto.
> La empresa ficticia de este caso se llama "FirmaYa S.A.S." para evitar confusiones.
> El objetivo es mostrar exactamente qué output produce el perfil legal ante una expansión
> internacional desde Argentina.

---

## 1. Descripción del caso

| Campo                 | Detalle                                                                     |
| --------------------- | --------------------------------------------------------------------------- |
| **Empresa ficticia**  | FirmaYa S.A.S. (CUIT 30-71543210-8)                                         |
| **Producto**          | SaaS de firma digital y gestión documental: firma electrónica con valor legal, flujos de aprobación, repositorio de contratos firmados |
| **Modelo de negocio** | B2B enterprise — clientes: empresas medianas y grandes en Argentina          |
| **Situación actual**  | Operando en Argentina desde 2021, 80 clientes enterprise, 12.000 usuarios activos |
| **Objetivo**          | Expansión a Chile, Colombia y Brasil en los próximos 18 meses                |
| **Infraestructura**   | AWS sa-east-1 (São Paulo, Brasil) — ya eligieron Brasil para minimizar latencia |
| **Firma digital**     | Infraestructura PKI propia + integración con AFIP (Argentina) para firma con CUIT |

### 1.1 Datos tratados (situación actual, solo Argentina)

- Nombre, DNI/CUIL, email, cargo, empresa del firmante
- Documentos firmados (pueden contener información confidencial de los clientes)
- Registros de auditoría de firma: IP, timestamp, hash del documento, coordenadas geográficas
- Certificados digitales de los firmantes

---

## 2. Variables de configuración

### Estado actual (solo Argentina)

```yaml
PAISES_OPERACION_ACTUAL:
  - AR

MODELO_NEGOCIO: "B2B_enterprise"
JURISDICCION_CLIENTES: "Argentina"
DATOS_TRATADOS:
  - datos_identificacion_firmantes
  - documentos_con_posible_contenido_sensible
  - registros_auditoria_firma
INFRAESTRUCTURA: "AWS sa-east-1 (São Paulo, Brasil)"
TRANSFERENCIA_A_BRASIL: true
INSCRIPCION_AAIP_AR: true  # Ya resuelta para operación Argentina
MARCO_FIRMA_DIGITAL_AR: "Ley 25.506"  # Ley de Firma Digital Argentina
```

### Estado proyectado (expansión)

```yaml
PAISES_OPERACION_PROYECTADA:
  - AR  # Ya operando
  - CL  # Chile — piloto Q1 próximo año
  - CO  # Colombia — piloto Q2 próximo año
  - BR  # Brasil — piloto Q3 próximo año
  - EU  # Posible: algunos clientes enterprise tienen filiales en la UE

MISMO_PRODUCTO_DIFERENTES_JURISDICCIONES: true
DOCUMENTACION_LEGAL_ACTUAL: "TyC + Privacy Policy solo para Argentina bajo Ley 25.326"
```

---

## 3. Análisis de qué cambia por país

### 3.1 Chile

**Marco vigente:**

Chile tiene la Ley 19.628 sobre Protección de la Vida Privada, sancionada en 1999.

[VERIFICAR VIGENCIA: Ley 19.628 Chile — existe un proyecto de ley de reforma de protección de datos personales que lleva varios años de tramitación parlamentaria y podría haber sido sancionado. El proyecto incorpora institutos similares al GDPR (consentimiento granular, DPO, notificación de brechas). Verificar si la reforma fue aprobada antes de usar este análisis.]

**Análisis bajo Ley 19.628 (si sigue vigente sin reforma):**

La Ley 19.628 es más básica que la Ley 25.326 argentina. Contempla:
- Principios de finalidad, pertinencia y consentimiento
- Derechos del titular: acceso, rectificación, cancelación
- Obligaciones de seguridad (menos detalladas que las argentinas)
- Autoridad de control: no hay agencia especializada; la supervisión recae principalmente en el Consejo para la Transparencia para el sector público y en los tribunales civiles para el sector privado

**Implicancias para FirmaYa:**

1. **Los TyC y Privacy Policy argentinos NO son válidos para Chile**: El vocabulario es diferente, las referencias normativas son diferentes (Ley 19.628 vs Ley 25.326), y los derechos del titular tienen plazos y canales distintos.

2. **Contratos con clientes chilenos**: Los contratos enterprise deben regirse por derecho chileno si los clientes son empresas chilenas. El DPA debe mencionar la Ley 19.628, no la Ley 25.326.

3. **Firma digital en Chile**: La firma electrónica avanzada en Chile se rige por la Ley 19.799 [VERIFICAR VIGENCIA]. FirmaYa necesita verificar si su PKI argentina tiene equivalencia o reconocimiento en Chile, o si debe integrarse con una entidad certificadora acreditada en Chile.

4. **Infraestructura en Brasil para clientes chilenos**: Los datos de personas chilenas almacenados en AWS sa-east-1 (São Paulo, Brasil) implican una transferencia internacional Chile → Brasil. Verificar qué mecanismo legitima esa transferencia bajo la Ley 19.628.

**Checklist mínimo antes de operar en Chile:**
- [ ] Adaptar Privacy Policy con vocabulario Ley 19.628 y contacto para ejercicio de derechos en Chile
- [ ] Redactar DPA para clientes chilenos bajo derecho chileno
- [ ] Verificar reconocimiento de firma digital argentina en Chile (Ley 19.799)
- [ ] Verificar si hay registro o notificación de bases de datos requerido en Chile
- [ ] Confirmar status de la reforma de ley de protección de datos (si fue aprobada, análisis completo cambia)

---

### 3.2 Colombia

**Marco vigente:**

Colombia tiene la Ley 1581/2012 sobre Protección de Datos Personales, reglamentada por los Decretos 1377/2013 y 886/2014, integrados en el Decreto Único Reglamentario 1074/2015.

[VERIFICAR VIGENCIA: Decretos reglamentarios bajo Ley 1581/2012 — verificar si hubo modificaciones o nuevas reglamentaciones de la Superintendencia de Industria y Comercio (SIC)]

La Superintendencia de Industria y Comercio (SIC) es la autoridad de protección de datos en Colombia. Tiene poderes sancionatorios significativos.

**Diferencias clave respecto a Argentina:**

| Aspecto                       | Argentina (Ley 25.326)          | Colombia (Ley 1581/2012)                |
| ----------------------------- | ------------------------------- | --------------------------------------- |
| Consentimiento                | Puede ser tácito en algunos casos | **Autorización previa, expresa e informada** — más estricta |
| Registro de bases de datos    | AAIP                            | **Registro Nacional de Bases de Datos (RNBD) ante SIC** |
| Aviso de privacidad           | Informar al recolectar          | **Aviso de privacidad previo** obligatorio |
| Derechos del titular          | Acceso, rectificación, supresión, confidencialidad | Acceso, rectificación, supresión, **queja ante SIC** |
| Transferencia internacional   | País con nivel adecuado o mecanismo | Similar, con control de SIC |
| Datos sensibles               | Régimen especial Ley 25.326     | **Prohibición por defecto**, con excepciones tasadas |

**Implicancias para FirmaYa:**

1. **Registro ante SIC obligatorio**: FirmaYa debe inscribir sus bases de datos en el Registro Nacional de Bases de Datos (RNBD) ante la SIC ANTES de empezar a operar en Colombia. Este registro es análogo al de la AAIP pero con requisitos propios.

2. **Autorización previa del titular**: El concepto colombiano de "autorización" es más estricto que el "consentimiento" argentino. Debe ser expresa, previa e informada. Además, la autorización debe conservarse por el responsable como prueba.

3. **Aviso de privacidad**: Antes de recolectar datos, FirmaYa debe informar al titular mediante un aviso de privacidad que incluya los datos del responsable, la finalidad del tratamiento, los derechos del titular y el mecanismo para ejercerlos.

4. **DPA con clientes colombianos**: Los clientes colombianos de FirmaYa son "responsables del tratamiento". FirmaYa es "encargada del tratamiento". El contrato debe regular esta relación bajo la Ley 1581/2012 (no bajo la Ley 25.326 argentina).

5. **Firma digital en Colombia**: Ley 527/1999 sobre comercio electrónico y firma digital en Colombia [VERIFICAR VIGENCIA]. Verificar equivalencia con PKI argentina.

**Checklist mínimo antes de operar en Colombia:**
- [ ] Inscribir bases de datos ante SIC (RNBD) antes de operar
- [ ] Redactar aviso de privacidad conforme Ley 1581/2012
- [ ] Redactar políticas de tratamiento de datos (documento más amplio que la Privacy Policy argentina)
- [ ] Adaptar flujo de onboarding para obtener "autorización" colombiana (más estricta que consentimiento argentino)
- [ ] Redactar DPA para clientes colombianos bajo derecho colombiano
- [ ] Verificar reconocimiento de firma digital argentina en Colombia

---

### 3.3 Brasil

**Marco vigente:**

Brasil tiene la Lei Geral de Proteção de Dados (LGPD), Lei 13.709/2018, en vigor desde septiembre de 2020. Es el equivalente brasileño del GDPR europeo.

[VERIFICAR VIGENCIA: LGPD y reglamentaciones de la ANPD — la Autoridade Nacional de Proteção de Dados (ANPD) ha emitido múltiples resoluciones y guías desde 2020. Verificar estado actual de la reglamentación sobre transferencias internacionales, DPO y notificación de incidentes.]

**Por qué la Privacy Policy argentina es insuficiente para Brasil:**

La LGPD exige elementos que la Privacy Policy bajo Ley 25.326 no contempla:

| Requisito LGPD                              | ¿Está en la PP argentina estándar? |
| ------------------------------------------- | ---------------------------------- |
| Base legal específica para cada tratamiento | No (la Ley 25.326 no requiere esto de forma tan granular) |
| DPO (Encarregado) para datos sensibles      | No aplica en Argentina             |
| Derechos del titular ampliados (portabilidad, revisión de decisiones automatizadas) | No (la Ley 25.326 no incluye portabilidad) |
| Notificación de incidente dentro de plazo específico a la ANPD | No aplica en Argentina |
| Referencia a la ANPD como autoridad de control | No (PP argentina menciona AAIP)  |
| Texto en idioma português                   | No (PP argentina está en español) |

**Elementos adicionales que requiere la LGPD:**

1. **Base legal por tratamiento** (art. 7 LGPD): A diferencia de Argentina, la LGPD exige identificar la base legal específica para cada tipo de tratamiento. Las bases legales son: consentimiento, cumplimiento de obligación legal, ejecución de contrato, ejercicio de derechos en proceso judicial, interés legítimo, entre otras. FirmaYa debe mapear cada tratamiento de datos con su base legal bajo LGPD.

2. **DPO / Encarregado** (art. 41 LGPD): Las empresas que traten datos a gran escala o datos sensibles deben designar un Encarregado (equivalente al DPO del GDPR). La ANPD puede exceptuar microempresas y startups, pero FirmaYa como B2B enterprise probablemente no califica como startup. [VERIFICAR VIGENCIA: resolución ANPD sobre excepciones al requisito de DPO]

3. **Notificación de incidente de seguridad** (art. 48 LGPD): En caso de brecha que pueda acarrear riesgo o daño a los titulares, FirmaYa debe notificar a la ANPD y a los titulares "en prazo razoável". La ANPD ha reglamentado este plazo. [VERIFICAR VIGENCIA: Resolução ANPD sobre prazo de notificação de incidentes]

4. **Transferencias internacionales** (art. 33 LGPD): La ANPD ha reglamentado las transferencias internacionales de datos. [VERIFICAR VIGENCIA: Resolução ANPD 19/2024 o la que esté vigente sobre transferencias internacionales — puede haber cambiado]. FirmaYa que almacena datos de brasileños en AWS sa-east-1 (São Paulo) no tiene problema de transferencia, pero si los datos salen hacia Argentina (ej: equipo de soporte accede a datos desde Argentina), eso es una transferencia internacional bajo LGPD.

5. **Direitos do titular** (art. 18 LGPD): Además de acceso, rectificación y supresión (similares a Argentina), la LGPD agrega: portabilidad de datos, información sobre con quién se comparten los datos, revocación del consentimiento y revisión de decisiones automatizadas. El canal de atención a titulares bajo LGPD tiene requisitos propios.

**Idioma:** Toda la documentación dirigida a usuarios brasileños (Privacy Policy, TyC, aviso de privacidad) debe estar en português. Una Privacy Policy en español no cumple el principio de transparencia bajo LGPD.

**Checklist mínimo antes de operar en Brasil:**
- [ ] Redactar Privacy Policy en português conforme LGPD
- [ ] Mapear bases legales de todos los tratamientos
- [ ] Designar Encarregado (DPO) o documentar por qué está exento
- [ ] Redactar DPA para clientes brasileños bajo LGPD (Contrato de Processamento de Dados)
- [ ] Adaptar canal de atención al titular con requisitos LGPD
- [ ] Diseñar procedimiento de notificación de incidentes a ANPD
- [ ] Verificar que el acceso desde Argentina a datos de brasileños tenga base bajo LGPD (transferencia internacional)
- [ ] Verificar equivalencia firma digital argentina en Brasil (MP 2.200-2/2001 ICP-Brasil) [VERIFICAR VIGENCIA]

---

### 3.4 Si también hay clientes con filiales o usuarios en la Unión Europea

**[ANÁLISIS — GDPR Y DECISIÓN DE ADECUACIÓN ARGENTINA]**

**Ventaja de Argentina:** Argentina tiene una decisión de adecuación de la Unión Europea desde 2003 (Decisión 2003/490/CE). Esto significa que las organizaciones en la UE pueden transferir datos personales a Argentina sin necesidad de mecanismos adicionales (como cláusulas contractuales tipo).

[VERIFICAR VIGENCIA: Decisión de adecuación UE-Argentina — la Comisión Europea ha revisado decisiones de adecuación previas (especialmente tras Schrems II). Verificar si la decisión argentina sigue vigente y si hay procedimiento de revisión en curso.]

**Sentido contrario — FirmaYa queda sujeta al GDPR si trata datos de personas en la UE:**

El GDPR aplica de forma extraterritorial (art. 3 GDPR). Si FirmaYa tiene clientes cuyas filiales en la UE usan la plataforma, o si empleados en la UE firman documentos en FirmaYa, FirmaYa queda sujeta al GDPR para esos tratamientos, independientemente de que sea una empresa argentina.

El GDPR aplicaría porque FirmaYa ofrecería "servicios a personas en la UE" (art. 3.2.a GDPR).

**Consecuencias de quedar bajo GDPR:**
- Privacy Policy adicional conforme GDPR (en el idioma del país de la filial o en inglés)
- Base legal GDPR para cada tratamiento
- DPO si el volumen lo requiere
- Representante en la UE (art. 27 GDPR) — empresa o persona física designada como punto de contacto para la autoridad de supervisión
- Notificación de brechas a la autoridad de supervisión en 72 horas

---

## 4. Checklist consolidado de expansión

### Antes de abrir el producto en cada nuevo país:

| Tarea                                                    | AR (ya hecho) | CL | CO | BR | UE (si aplica) |
| -------------------------------------------------------- | :-----------: | :--: | :--: | :--: | :--: |
| Privacy Policy adaptada al marco local                   | ✓ | - | - | - | - |
| TyC adaptados al marco local (idioma + normativa)        | ✓ | - | - | - | - |
| DPA para clientes bajo derecho local                     | ✓ | - | - | - | - |
| Registro/inscripción ante autoridad de control local     | ✓ AAIP | Verificar | SIC | ANPD | No aplica (decisión adecuación) |
| Mecanismo de legitimación transferencia internacional    | Verificar AWS BR | Verificar | Verificar | AWS SP local | Decisión adecuación |
| Verificación equivalencia firma digital                  | ✓ Ley 25.506 | Ley 19.799 | Ley 527/1999 | MP 2.200-2/2001 | eIDAS |
| Canal de habeas data / derechos del titular local        | ✓ | - | - | - | - |
| Contrato de trabajo/servicios con equipo local           | ✓ | - | - | - | - |
| Abogado local revisando documentación                    | ✓ | - | - | - | - |

---

## 5. Consulta de ejemplo al modelo con el perfil cargado

### Pregunta del usuario (CEO o abogado de FirmaYa):

> "Vamos a hacer un piloto en Colombia con 3 clientes enterprise. Son empresas colombianas grandes. Queremos empezar en 60 días. ¿Qué necesitamos adaptar de nuestra documentación legal actual (que está toda pensada para Argentina)?"

### Respuesta esperada del modelo con el perfil check-legal-saas-ar cargado:

```
Para un piloto en Colombia con clientes enterprise en 60 días,
la documentación argentina NO sirve. Hay que producir documentación
nueva. Esto es lo que necesitan resolver:

URGENTE — SIN ESTO NO PUEDEN OPERAR LEGALMENTE:

1. INSCRIPCIÓN ANTE SIC (Registro Nacional de Bases de Datos)
   Colombia exige registrar las bases de datos ante la SIC ANTES
   de empezar a tratar datos de personas colombianas. El trámite
   es online pero tiene tiempos de procesamiento. Iniciar YA.
   [Ley 1581/2012 + Decreto 090/2018 — VERIFICAR VIGENCIA]

2. POLÍTICA DE TRATAMIENTO DE DATOS (no es lo mismo que la
   Privacy Policy argentina)
   Colombia exige un documento más amplio que contemple:
   - Datos del responsable (Ustedes como FirmaYa) con domicilio
   - Finalidades del tratamiento
   - Derechos del titular y cómo ejercerlos
   - Vigencia de la política
   - Procedimiento para atender consultas y reclamos
   Este documento debe estar en español colombiano y publicado
   en el sitio web antes de recolectar datos.

3. AVISO DE PRIVACIDAD PREVIO
   Antes de recolectar cualquier dato de personas en Colombia
   (incluyendo los contactos de los clientes enterprise),
   deben enviar un aviso de privacidad. No alcanza con que
   esté en los TyC: debe ser previo a la recolección.

4. CONTRATO / DPA CON CLIENTES COLOMBIANOS
   El DPA argentino no sirve para clientes colombianos.
   Necesitan un "Contrato de Encargado de Tratamiento" bajo
   Ley 1581/2012 que regule:
   - FirmaYa como encargada del tratamiento
   - El cliente colombiano como responsable
   - Las obligaciones de FirmaYa respecto a la SIC
   - Qué pasa con los datos al finalizar el contrato

IMPORTANTE PERO PUEDE HACERSE EN PARALELO:

5. MECANISMO DE TRANSFERENCIA COLOMBIA → BRASIL
   Los datos de personas colombianas se van a almacenar en
   AWS sa-east-1 (São Paulo). Eso es una transferencia
   internacional de Colombia a Brasil. Necesitan identificar
   el mecanismo de legitimación bajo la Ley 1581/2012
   (declaración de conformidad o cláusulas contractuales).

6. FLUJO DE "AUTORIZACIÓN" PARA FIRMANTES COLOMBIANOS
   La Ley 1581/2012 usa el concepto de "autorización" que es
   más estricto que el consentimiento argentino. Los firmantes
   de documentos en Colombia deben dar una autorización previa,
   expresa e informada para que sus datos (nombre, CUIL/NIT,
   email, registro de firma) sean tratados por FirmaYa.
   Esto requiere adaptar el flujo de onboarding de firmantes.

LO QUE NO CAMBIA:
- La infraestructura en AWS sa-east-1 sirve (Colombia está
  geográficamente razonable, baja latencia hacia São Paulo)
- El producto en sí no necesita cambios técnicos para el piloto
- La misma lógica de auditoría de firma sirve

ESTIMADO REALISTA: 60 días son ajustados pero posibles si
tienen abogado local colombiano desde esta semana. El punto
crítico es el registro ante SIC: si hay demoras en la tramitación,
el piloto se atrasa.
```

---

*Licencia: Apache 2.0 — ver LICENSE en la raíz del repositorio.*
*Este caso es completamente ficticio. No constituye asesoramiento legal.*
*[VERIFICAR VIGENCIA: Ley 19.628 Chile y proyecto de reforma]*
*[VERIFICAR VIGENCIA: Ley 19.799 Chile sobre firma electrónica]*
*[VERIFICAR VIGENCIA: Ley 1581/2012 Colombia y decretos reglamentarios — Decreto 090/2018 SIC]*
*[VERIFICAR VIGENCIA: LGPD Brasil — Resoluciones ANPD sobre DPO, transferencias internacionales y notificación de incidentes]*
*[VERIFICAR VIGENCIA: MP 2.200-2/2001 ICP-Brasil sobre firma digital]*
*[VERIFICAR VIGENCIA: Decisión de adecuación UE-Argentina 2003/490/CE — verificar si sigue vigente]*
