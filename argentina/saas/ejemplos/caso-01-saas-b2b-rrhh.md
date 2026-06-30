# Caso 01 — SaaS B2B de RRHH: "TalentoAR"

> Caso ficticio. Empresa, nombre, CUIL y datos inventados. El objetivo es mostrar
> exactamente qué output produce el perfil legal ante este tipo de producto.

---

## 1. Descripción del caso

| Campo                  | Detalle                                                                    |
| ---------------------- | -------------------------------------------------------------------------- |
| **Empresa ficticia**   | TalentoAR S.A.S. (CUIT 30-71234567-0)                                     |
| **Producto**           | Plataforma SaaS de gestión de RRHH: legajos digitales, liquidación de haberes, control de asistencia, gestión de licencias y certificados médicos |
| **Modelo de negocio**  | B2B — clientes: empresas medianas (50-500 empleados); usuarios finales: área de RRHH de cada empresa cliente |
| **Precio**             | Suscripción mensual por empresa + por cantidad de empleados activos         |
| **Datos tratados**     | Ver sección 1.1                                                            |
| **Infraestructura**    | AWS us-east-1 (Virginia, EE.UU.) + CDN CloudFront                         |
| **Soporte**            | Equipo en Argentina + partner de soporte en Uruguay                        |

### 1.1 Catálogo de datos tratados

**Datos comunes de empleados (art. 2 Ley 25.326):**
- Nombre completo, DNI, CUIL
- Domicilio, teléfono, email
- Fecha de nacimiento, estado civil
- Datos bancarios (CBU para acreditación de haberes)
- Historial laboral, cargo, categoría, antigüedad

**Datos sensibles (art. 2 Ley 25.326 — régimen especial art. 7):**
- Certificados y diagnósticos médicos (licencias por enfermedad)
- Certificados de discapacidad (ANDIS)
- Afiliación sindical (para descuentos de cuota sindical)
- Licencias por maternidad/paternidad (puede revelar datos de salud)

---

## 2. Variables de configuración para el perfil

```yaml
# Estas variables se cargan en el perfil check-legal-saas-ar
# antes de iniciar la sesión de consulta

MODELO_NEGOCIO: "B2B"
TIPO_CLIENTES: "empresas_medianas"
USUARIOS_FINALES: "empleados_de_clientes_empresa"
ROL_EN_EL_DATO: "usuario_del_dato"  # TalentoAR no es responsable del archivo

DATOS_COMUNES:
  - nombre_dni_cuil
  - domicilio_contacto
  - datos_bancarios
  - historial_laboral

DATOS_SENSIBLES:  # art. 2 Ley 25.326
  - certificados_medicos_diagnosticos
  - certificados_discapacidad
  - afiliacion_sindical

TRANSFERENCIAS_INTERNACIONALES: true
DESTINO_TRANSFERENCIA: "AWS us-east-1 (EE.UU.)"
NIVEL_ADECUACION_DESTINO: null  # EE.UU. no tiene nivel adecuado reconocido por Argentina

JURISDICCION_CLIENTES: "Argentina"
JURISDICCION_USUARIOS_FINALES: "Argentina"

TIENE_DPA_CON_CLIENTES: null  # A verificar — ver red-flags
TIENE_INSCRIPCION_AAIP: null  # A verificar
```

---

## 3. Análisis que produce el perfil

### 3.1 Alerta crítica — Datos sensibles: régimen especial art. 7 Ley 25.326

**[ALERTA CRÍTICA — DATOS SENSIBLES]**

TalentoAR trata datos sensibles de los empleados de sus clientes: certificados médicos, diagnósticos, certificados de discapacidad y afiliación sindical. Esto activa el régimen especial del art. 7 Ley 25.326:

> Art. 7 Ley 25.326: "Ninguna persona puede ser obligada a proporcionar datos sensibles. Los datos sensibles sólo pueden ser recolectados y objeto de tratamiento cuando medien razones de interés general autorizadas por ley. También podrán ser tratados con finalidades estadísticas o científicas cuando no puedan ser identificados sus titulares."

**Consecuencia directa para TalentoAR:**

El consentimiento que los empleados del cliente dan a su *empleador* (empresa cliente) para el tratamiento de su legajo es insuficiente para autorizar que TalentoAR acceda y procese esos datos sensibles. El empleado del cliente NO es parte del contrato entre TalentoAR y la empresa cliente.

El tratamiento de datos sensibles sin base legal válida configura infracción a la Ley 25.326. Las sanciones van desde apercibimiento hasta multa (art. 31 Ley 25.326) y eventual inhabilitación.

**Base legal posible para datos sensibles en este contexto:**
- Consentimiento expreso del titular (el empleado) informado específicamente sobre el tratamiento por TalentoAR — difícil de obtener a escala
- Obligación legal del empleador (ej: el empleador está obligado por ley a conservar registros médicos) — puede amparar el almacenamiento pero no necesariamente el tratamiento por un tercero SaaS
- Requiere análisis legal específico caso por caso

---

### 3.2 Obligación AAIP — Inscripción de base de datos

**[OBLIGACIÓN — INSCRIPCIÓN AAIP]**

Ley 25.326 art. 21: Todo archivo, registro, base o banco de datos de carácter personal debe inscribirse en el Registro Nacional de Bases de Datos de la AAIP (Agencia de Acceso a la Información Pública).

TalentoAR debe inscribir:
- Base de datos "Empleados de clientes" — datos comunes + datos sensibles
- Base de datos "Contactos comerciales" — datos de los usuarios del área de RRHH de cada empresa cliente
- Potencialmente: base de datos "Prospectos" si tiene CRM con datos de personas físicas

La inscripción no es automática ni instantánea. Hay que tramitarla ante la AAIP con anterioridad al inicio del tratamiento, no después.

[VERIFICAR VIGENCIA: Disposición AAIP sobre procedimiento de inscripción — verificar si el trámite sigue siendo 100% online o requiere pasos presenciales]

---

### 3.3 Transferencia internacional a EE.UU. — Sin nivel adecuado

**[ALERTA — TRANSFERENCIA INTERNACIONAL SIN NIVEL ADECUADO]**

La Resolución AAIP 159/2018 [VERIFICAR VIGENCIA] establece los países con nivel adecuado de protección de datos reconocido por Argentina. **EE.UU. no está en esa lista.**

El art. 12 Ley 25.326 prohíbe la transferencia internacional de datos personales hacia países que no tengan nivel adecuado, salvo excepciones tasadas:

- Colaboración judicial internacional
- Razones de interés público
- **Consentimiento del titular** — válido pero difícil a escala
- **Cláusulas contractuales tipo** — requieren análisis de validez bajo derecho argentino
- El país destinatario garantiza nivel adecuado por otro mecanismo

**Para TalentoAR:**

El mero uso de AWS us-east-1 no legitima por sí solo la transferencia. Opciones a evaluar:
1. Migrar a AWS sa-east-1 (São Paulo, Brasil) — reduce el problema pero no lo elimina por completo (Brasil tiene LGPD, no hay decisión de adecuación Argentina-Brasil)
2. Usar AWS us-east-1 con cláusulas contractuales tipo acordadas con AWS — verificar validez bajo ley argentina
3. Obtener consentimiento expreso de cada titular para la transferencia — operativamente complejo
4. Consultar con abogado especializado en transferencias internacionales bajo Ley 25.326

[VERIFICAR VIGENCIA: Lista de países con nivel adecuado según AAIP — puede haber actualizaciones]

---

### 3.4 DPA obligatorio con cada cliente empresarial

**[OBLIGACIÓN — DATA PROCESSING AGREEMENT (DPA) CON CLIENTES B2B]**

En el modelo B2B de TalentoAR:

- **La empresa cliente** es el *responsable del archivo* (art. 2 Ley 25.326): decide qué datos de sus empleados recopilar y con qué finalidad
- **TalentoAR** es el *usuario del dato* (art. 2 Ley 25.326): trata los datos por cuenta y bajo instrucción del cliente

Esta distinción es fundamental. El cliente empresarial le encomienda a TalentoAR el tratamiento de datos de los empleados del cliente. Eso requiere un contrato específico (en la práctica internacional: Data Processing Agreement o DPA) que regule:

- Finalidades del tratamiento (solo las instrucciones del cliente)
- Obligaciones de confidencialidad del personal de TalentoAR que acceda a los datos
- Obligaciones de seguridad (medidas técnicas y organizativas)
- Condiciones para la subcontratación (ej: AWS como sub-encargado)
- Qué hace TalentoAR con los datos si el cliente rescinde el contrato
- Procedimiento ante solicitudes de habeas data de empleados del cliente
- Procedimiento ante brechas de seguridad (notificación al cliente)

Si los contratos actuales de TalentoAR con sus clientes son simples contratos de software/servicio SaaS sin estas cláusulas, hay un problema legal significativo.

---

### 3.5 Medidas de seguridad — Nivel ALTO por datos sensibles

**[OBLIGACIÓN — MEDIDAS DE SEGURIDAD NIVEL ALTO]**

Disposición AAIP 47/2018 (antes Disposición DNPDP 11/2006) [VERIFICAR VIGENCIA: número de disposición vigente] establece niveles de seguridad para bases de datos personales:

| Nivel | Cuándo aplica                                      | Medidas mínimas                               |
| ----- | -------------------------------------------------- | --------------------------------------------- |
| BAJO  | Solo datos identificativos básicos                 | Control de acceso, registro de incidentes     |
| MEDIO | Datos personales en general                        | Nivel bajo + cifrado en tránsito, auditoría   |
| ALTO  | Datos sensibles, financieros, datos de menores     | Nivel medio + cifrado en reposo, test de penetración anual, registro de accesos detallado, pseudonimización |

TalentoAR trata datos sensibles → **Nivel ALTO obligatorio**.

Esto implica, entre otras cosas:
- Cifrado en reposo de los datos sensibles en la base de datos (no solo en tránsito)
- Registro de auditoría de quién accedió a qué datos sensibles y cuándo
- Procedimiento documentado de respuesta ante brechas de seguridad
- Test de penetración con periodicidad documentada
- Control de accesos por rol (el área de RRHH del cliente solo ve sus propios empleados)

---

## 4. Red-flags específicas del caso

### RF-01: ¿Los contratos con clientes B2B incluyen DPA?

```
PREGUNTA: ¿El contrato estándar de TalentoAR con sus clientes
          empresariales incluye cláusulas de procesamiento de datos
          (DPA) según art. 2 Ley 25.326?

SI NO → [RED FLAG — RIESGO ALTO]
         El cliente y TalentoAR están tratando datos de los empleados
         del cliente sin marco contractual que delimite responsabilidades.
         En caso de brecha o reclamo de habeas data, la exposición legal
         de ambas partes es significativa.

CORRECCIÓN: Incorporar DPA al contrato estándar o como addendum.
            El DPA debe estar vigente ANTES de que el cliente empiece
            a cargar datos en la plataforma.
```

### RF-02: ¿Los empleados del cliente dieron consentimiento para el tratamiento de sus datos sensibles por TalentoAR?

```
PREGUNTA: ¿Los empleados de las empresas clientes de TalentoAR
          dieron consentimiento expreso e informado para que
          TalentoAR (como tercero) trate sus datos de salud
          (certificados médicos, diagnósticos, discapacidad)?

SI NO → [RED FLAG — RIESGO DE NULIDAD: art. 7 Ley 25.326]
         El tratamiento de datos sensibles sin base legal válida
         es ilícito bajo la Ley 25.326. El consentimiento dado
         al empleador no se traslada automáticamente a TalentoAR.

POSIBLES CORRECCIONES:
  a) Diseñar flujo de consentimiento expreso en el onboarding del
     empleado en la plataforma, con información clara sobre quién
     trata los datos (TalentoAR + AWS us-east-1)
  b) Restringir el tratamiento de datos sensibles a lo estrictamente
     necesario para la obligación legal del empleador (ej: solo
     guardar el número de certificado y días de licencia, no el
     diagnóstico)
  c) Consultar con abogado si la base legal puede ser "obligación
     legal del empleador" en lugar de consentimiento
```

### RF-03: ¿El contrato con desarrolladores y colaboradores incluye cesión de IP?

```
PREGUNTA: ¿Los contratos con desarrolladores, diseñadores y
          cualquier colaborador que haya contribuido al código
          de TalentoAR incluyen cláusula de cesión de derechos
          de propiedad intelectual?

SI NO → [RED FLAG — RIESGO ALTO: Ley 11.723]
         Bajo la Ley 11.723, los derechos de autor sobre el software
         pertenecen por defecto al autor (la persona física), no a
         quien contrató el desarrollo.
         Un desarrollador freelance o contratado sin cláusula de
         cesión podría reclamar derechos sobre el código que produjo.

CORRECCIÓN: Agregar cláusula de cesión de derechos de propiedad
            intelectual en todos los contratos de trabajo y de
            servicios de desarrollo. Para contratos ya existentes:
            firmar addendum de cesión retroactiva (requiere
            consentimiento del autor).
```

### RF-04: ¿La política de privacidad menciona a AWS como destinatario de transferencia internacional?

```
PREGUNTA: ¿La política de privacidad de TalentoAR informa
          a los titulares de datos que sus datos se transfieren
          a EE.UU. (AWS us-east-1)?

SI NO → [RED FLAG — RIESGO MEDIO: art. 6 Ley 25.326]
         El principio de información (art. 6) exige que el titular
         sepa quién trata sus datos, con qué finalidad y si habrá
         transferencias internacionales.

CORRECCIÓN: Actualizar política de privacidad para mencionar:
            - AWS como proveedor de infraestructura
            - Que los datos se almacenan en EE.UU.
            - El mecanismo de legitimación de la transferencia
            - Los derechos del titular y el canal de habeas data
```

---

## 5. Consulta de ejemplo al modelo con el perfil cargado

### Pregunta del usuario (abogado o founder de TalentoAR):

> "Nuestros clientes son empresas que tienen entre 100 y 300 empleados. Los clientes cargan en nuestra plataforma los certificados médicos de sus empleados para gestionar las licencias. ¿Necesitamos algún permiso especial para almacenar esos certificados?"

### Respuesta esperada del modelo con el perfil check-legal-saas-ar cargado:

```
Sí. Los certificados médicos son datos sensibles bajo el art. 2 de la
Ley 25.326 porque revelan información de salud. Eso activa el régimen
especial del art. 7 y tiene consecuencias concretas para ustedes:

1. CONSENTIMIENTO DEL TITULAR: El empleado (no la empresa cliente)
   es el titular del dato. El consentimiento que el empleado le dio
   a su empleador para el uso de su legajo no los habilita a ustedes
   (TalentoAR) a tratar esos datos. Necesitan base legal propia.
   La más limpia: consentimiento expreso del empleado informándole
   que TalentoAR almacena el certificado en AWS EE.UU.

2. CONTRATO CON EL CLIENTE: El contrato que tienen con la empresa
   cliente necesita un addendum de procesamiento de datos (DPA) que
   establezca que ustedes tratan los datos por cuenta e instrucción
   del cliente (que es el responsable del archivo). Sin ese DPA,
   la responsabilidad está indefinida en caso de reclamo.

3. INSCRIPCIÓN AAIP: La base de datos que contiene los certificados
   médicos debe estar inscripta ante la AAIP antes de que empiecen
   a almacenar esos datos. Si ya la están usando sin inscripción,
   están en infracción.

4. SEGURIDAD NIVEL ALTO: Los datos de salud requieren nivel ALTO
   de seguridad según la Disposición AAIP 47/2018. Eso incluye
   cifrado en reposo, auditoría de accesos y test de penetración
   periódico — no solo HTTPS.

5. TRANSFERENCIA A EE.UU.: AWS us-east-1 está en EE.UU., que no
   tiene nivel adecuado reconocido por Argentina. Necesitan un
   mecanismo de legitimación para esa transferencia (ej: cláusulas
   contractuales, consentimiento expreso del titular).

Recomendación inmediata: no ampliar el módulo de certificados médicos
hasta resolver los puntos 1 y 2. El riesgo regulatorio de almacenar
datos sensibles sin base legal es alto.
```

---

*Licencia: Apache 2.0 — ver LICENSE en la raíz del repositorio.*
*Este caso es completamente ficticio. No constituye asesoramiento legal.*
*[VERIFICAR VIGENCIA: Disposición AAIP 47/2018 sobre medidas de seguridad]*
*[VERIFICAR VIGENCIA: Resolución AAIP 159/2018 sobre países con nivel adecuado]*
