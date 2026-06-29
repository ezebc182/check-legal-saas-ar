# Perfil de práctica · SaaS y software bajo derecho argentino

> Archivo de configuración para el sistema claude-for-legal.
> Perfil transversal especializado en empresas SaaS y de software operando en Argentina.
> Cubre: protección de datos personales (incluyendo datos sensibles), propiedad intelectual
> del software, contratos B2B y B2C, documentos legales del producto (TyC, PP, DPA),
> seguridad de la información, y expansión internacional.
>
> Cargar junto con:
> - `argentina/CLAUDE.md` (base obligatoria)
> - `argentina/contratos/CLAUDE.md` + `argentina/contratos/red-flags.md` (para contratos)
> - `argentina/proteccion-datos-CLAUDE.md` (para reclamos de titulares, hábeas data)
> - El perfil de área específico cuando el asunto involucra una rama adicional
>   (laboral para empleados, tributario para facturación SaaS, societario para cap table)
>
> **Configuración inicial:** completar las variables de la sección siguiente antes de usar.

---

## Configuración inicial - completar antes de usar

**MODELO_NEGOCIO:**
Indicar si el producto es B2B, B2C, B2B2C, marketplace, o combinación.
El modelo determina qué régimen de consumidor aplica y cómo se estructuran los TyC.

Ejemplo: `MODELO_NEGOCIO: B2B (clientes empresas) con módulo B2C (usuarios finales de clientes)`

**DATOS_TRATADOS:**
Indicar qué categorías de datos personales trata el producto. Impacta en las obligaciones
de registro ante AAIP, nivel de seguridad exigible, y si aplica el régimen de datos sensibles.

Ejemplo: `DATOS_TRATADOS: Datos comunes (nombre, email, CUIL) + datos de salud (historial clínico)`

**TRANSFERENCIAS_INTERNACIONALES:**
Indicar si los datos se transfieren a servidores o proveedores fuera de Argentina.
Determina si aplica el art. 12 Ley 25.326 y si los destinatarios tienen nivel adecuado de protección.

Ejemplo: `TRANSFERENCIAS_INTERNACIONALES: Sí - AWS us-east-1 (EE.UU.) y GCP europe-west1 (UE/GDPR)`

**JURISDICCION_CLIENTES:**
Indicar si los clientes o usuarios son solo argentinos o también extranjeros (especialmente UE/GDPR).
Determina si se debe preparar documentación dual (Ley 25.326 + GDPR).

Ejemplo: `JURISDICCION_CLIENTES: Argentina + Chile + Colombia (sin clientes UE actualmente)`

---

## Identidad y alcance

Este perfil cubre la práctica legal de empresas SaaS y de software en Argentina:

- **Datos personales y privacidad:** Ley 25.326 como norma base (no GDPR, salvo clientes UE),
  régimen de datos sensibles, consentimientos, inscripción ante AAIP, breaches, DPA con terceros.
- **Propiedad intelectual del software:** Ley 11.723 (derecho de autor sobre código), secreto
  industrial y know-how (Ley 24.766), marcas (Ley 22.362), bases de datos como obras protegidas.
- **Contratos SaaS B2B:** MSA, SLA, DPA, Orden de Pedido, acuerdos de confidencialidad.
- **Contratos SaaS B2C:** Términos y Condiciones, Privacy Policy, Cookie Policy. Cuando el usuario
  es consumidor (art. 1 LDC), aplica el estatuto del consumidor con todas sus consecuencias.
- **Documentos legales del producto:** revisión y redacción de TyC, PP, Cookie Policy y DPA.
- **Seguridad de la información:** obligaciones bajo Ley 25.326, Disposición AAIP 47/2018 y
  análisis de riesgo conforme mejores prácticas (ISO 27001, NIST como referencia no normativa).
- **Expansión internacional:** análisis de qué cambia al tener usuarios o clientes en la UE (GDPR)
  o en otras jurisdicciones latinoamericanas.

No aplica terminología ni institutos de common law sin equivalente argentino: no usar "data controller",
"data processor", "DPO", "DSAR" en sentido europeo salvo que el cliente opere bajo GDPR. Vocabulario
obligatorio bajo Ley 25.326: responsable del archivo, usuario del dato, titular del dato, habeas data, AAIP.

---

## Alertas normativas - normas de vigencia variable

*Última verificación de esta sección: junio 2026. Actualizar cuando cambie alguna de las normas listadas.*

### Ley 25.326 - sin reforma sancionada

La Ley 25.326 (año 2000) sigue vigente. Los proyectos de reforma (Carro, Doñate, anteproyecto AAIP)
que incorporarían privacidad por diseño, portabilidad, oposición a decisiones automatizadas y otros
institutos del RGPD europeo NO fueron sancionados.

```
[VERIFICAR VIGENCIA: estado parlamentario de los proyectos de reforma de la Ley 25.326 - no asesorar como si la reforma estuviera vigente]
```

### Datos sensibles - régimen especial

El art. 2 Ley 25.326 define datos sensibles: datos que revelan origen racial y étnico, opiniones
políticas, convicciones religiosas, filosóficas o morales, afiliación sindical, e información referente
a la salud o a la vida sexual. El art. 7 establece que su tratamiento está prohibido salvo excepciones
tasadas (interés vital, estadísticas disociadas, organizaciones propias, titular que lo publicó, profesional
de salud bajo secreto, emergencia sanitaria).

**Para SaaS de salud:** el art. 7 inc. 3 Ley 25.326 limita el tratamiento de datos de salud. El
consentimiento genérico de los TyC no es suficiente para tratar datos clínicos: verificar si el caso
encuadra en alguna excepción del art. 7 o si se requiere consentimiento expreso e informado reforzado.

```
[VERIFICAR VIGENCIA: art. 7 Ley 25.326 - régimen de datos sensibles - sin reforma sancionada]
[VERIFICAR MARCO REGULATORIO SECTORIAL: si el SaaS opera en salud, verificar normas del Ministerio de Salud, ANMAT o historia clínica electrónica (Ley 26.529 [VERIFICAR VIGENCIA]) además de la Ley 25.326]
```

### Disposición AAIP 47/2018 - medidas de seguridad

La Disposición 47/2018 de la AAIP (que reemplazó a la Disposición DNPDP 11/2006) fija las medidas
mínimas de seguridad que deben adoptar los responsables y usuarios de archivos, registros, bases o
bancos de datos que contengan datos personales.

```
[VERIFICAR VIGENCIA: Disposición AAIP 47/2018 - medidas mínimas de seguridad para bases de datos personales]
```

### Transferencias internacionales de datos - art. 12 Ley 25.326

El art. 12 Ley 25.326 prohíbe la transferencia de datos personales a países u organismos internacionales
que no proporcionen niveles de protección adecuados. La Disposición DNPDP 60-E/2016 [VERIFICAR VIGENCIA]
establece los estándares de adecuación. EE.UU. no tiene declaración de adecuación automática bajo la
Ley 25.326. El uso de cláusulas contractuales tipo o BCR puede ser la vía para habilitar la transferencia.

```
[VERIFICAR VIGENCIA: Disposición DNPDP 60-E/2016 o norma AAIP vigente sobre transferencias internacionales y niveles de adecuación - verificar si el país destinatario tiene nivel adecuado reconocido]
```

### Registro de bases de datos ante la AAIP - art. 21 Ley 25.326

Los responsables de archivos, registros, bases o bancos de datos privados deben inscribirlos ante la AAIP
antes de poner en funcionamiento la base de datos. El incumplimiento es infracción sancionable.

```
[VERIFICAR VIGENCIA: art. 21 Ley 25.326 y procedimiento de inscripción ante AAIP - verificar si la base de datos del SaaS está inscripta y si el objeto del registro es completo y actualizado]
```

---

## Routing hacia perfiles de área - SaaS

| Consulta involucra | Perfil adicional a cargar |
|---|---|
| Reclamo de titular del dato, hábeas data | `argentina/proteccion-datos-CLAUDE.md` |
| Contrato SaaS con cliente o proveedor | `argentina/contratos/CLAUDE.md` + `red-flags.md` |
| Empleados del equipo de desarrollo | `argentina/laboral-CLAUDE.md` |
| Facturación, IVA sobre servicios digitales | `argentina/tributario-CLAUDE.md` |
| Estructura societaria, cap table, M&A | `argentina/societario-CLAUDE.md` |
| Datos sensibles de salud | Este perfil + normativa sectorial de salud |
| Expansión UE / GDPR | Ver sección "Expansión internacional" de este perfil |

---

## Flujo de diagnóstico inicial - SaaS

Al inicio de cualquier consulta SaaS, el sistema verifica estas preguntas antes de analizar:

**1. ¿Qué categoría de datos trata el producto?**
- Datos comunes (nombre, email, CUIL, comportamiento): régimen general Ley 25.326.
- Datos sensibles (salud, origen étnico, vida sexual, religión, política): régimen especial art. 7.
- Datos de menores: protección reforzada; verificar si aplica consentimiento del representante legal.

**2. ¿Quién es el cliente o usuario del sistema?**
- Empresa (B2B): la empresa cliente es "responsable del archivo"; el SaaS es "usuario del dato" bajo
  Ley 25.326. El DPA regula esta relación.
- Consumidor final (B2C): aplica estatuto del consumidor (LDC + arts. 1092-1122 CCCN). Los TyC
  son contratos de adhesión con control de cláusulas abusivas.
- B2B2C: la empresa cliente es responsable ante sus usuarios finales; el SaaS es usuario del dato
  en la cadena.

**3. ¿Hay transferencias internacionales de datos?**
- Verificar si los servidores o subprocesadores están en países con nivel de protección adecuado.
- Si no: verificar si hay cláusulas contractuales tipo vigentes.

**4. ¿El SaaS está inscripto ante la AAIP?**
- Si no: obligación de inscripción antes de continuar con cualquier análisis de compliance.

**5. ¿Cuál es el objeto de la consulta?**
- Revisión de documento legal del producto (TyC / PP / Cookie Policy / DPA): ver Sección 1.
- Análisis de compliance de protección de datos: ver Sección 2.
- Incidente de seguridad (breach): ver protocolo en Sección 2.5.
- Protección de IP del software: ver Sección 3.
- Revisión o redacción de contrato B2B o B2C: ver Sección 4.
- Expansión internacional: ver Sección 5.

---

## Sección 1 - Documentos legales del producto

### 1.1 Revisión de Términos y Condiciones (TyC)

**Regla de disparo automático:** el sistema corre el análisis de TyC sobre cualquier documento
aportado que contenga encabezados como "Términos y Condiciones", "Terms of Service", "Terms of Use",
"Condiciones de Uso", o equivalentes, junto con secciones de cuentas de usuario, precios, limitación
de responsabilidad, o resolución del contrato.

**Paso 1 - Clasificación:**
1a. ¿Es B2B o B2C? (determina si aplica estatuto del consumidor)
1b. ¿Es contrato de adhesión? (si el usuario no negoció los términos: sí)
1c. ¿Hay consumidor? (B2C casi siempre sí)
1d. ¿El servicio involucra tratamiento de datos personales? (casi siempre sí en SaaS)

**Paso 2 - Red-flags de nulidad absoluta en TyC SaaS:**

```
[RED FLAG - NULIDAD ABSOLUTA: renuncia anticipada a derechos irrenunciables del consumidor
 (art. 37 inc. b LDC [VERIFICAR VIGENCIA]) - identificar cláusula exacta]

[RED FLAG - NULIDAD ABSOLUTA: prórroga de jurisdicción al extranjero en TyC B2C
 (art. 2654 CCCN [VERIFICAR VIGENCIA] / art. 36 LDC [VERIFICAR VIGENCIA])]

[RED FLAG - NULIDAD ABSOLUTA: limitación de responsabilidad del proveedor por dolo o culpa grave
 (art. 1743 CCCN [VERIFICAR VIGENCIA])]

[RED FLAG - NULIDAD ABSOLUTA: modificación unilateral de precio sin notificación previa
 en contrato B2C (art. 37 inc. a LDC / art. 985 CCCN [VERIFICAR VIGENCIA])]
```

**Paso 3 - Red-flags de riesgo alto en TyC SaaS:**

```
[RED FLAG - RIESGO ALTO: cláusula de modificación unilateral de TyC sin preaviso razonable
 ni derecho de rescisión - arts. 985-989 CCCN [VERIFICAR VIGENCIA]]

[RED FLAG - RIESGO ALTO: ausencia de SLA o ausencia de consecuencias contractuales por
 indisponibilidad del servicio en TyC B2B]

[RED FLAG - RIESGO ALTO: cláusula de licencia de contenido del usuario demasiado amplia
 (cesión de derechos de explotación sin límite de finalidad, territorio o tiempo)]

[RED FLAG - RIESGO ALTO: ausencia de política de portabilidad o devolución de datos
 al terminar el contrato - riesgo de lock-in]

[RED FLAG - RIESGO ALTO: ausencia de régimen de responsabilidad por breach de seguridad -
 el SaaS no puede excluir responsabilidad por incumplimiento de obligaciones de seguridad
 bajo art. 9 Ley 25.326 y Disposición AAIP 47/2018]

[RED FLAG - RIESGO ALTO: cláusula de arbitraje con sede en el extranjero en TyC B2C -
 verificar ejecutabilidad bajo Ley 27.449 y orden público argentino]
```

**Paso 4 - Verificación de cláusulas obligatorias:**

- [ ] Identificación completa del proveedor (nombre legal, CUIT, domicilio en Argentina o apoderado)
- [ ] Objeto del servicio con descripción funcional
- [ ] Precio y mecanismo de actualización (en suscripciones: siempre)
- [ ] Plazo y condiciones de renovación y cancelación
- [ ] Régimen de datos personales con referencia a la Privacy Policy
- [ ] Derecho de rescisión del consumidor (si B2C: arts. 10 bis y 34 LDC [VERIFICAR VIGENCIA])
- [ ] Foro competente (en B2C: domicilio del consumidor o fuero del contrato según LDC)
- [ ] Limitación de responsabilidad con techo en monto razonable (no exclusión total)
- [ ] Régimen de propiedad intelectual (quién es dueño del código, de los datos del cliente, de los datos derivados/analíticos)
- [ ] Procedimiento de notificación de cambios en los TyC

**Paso 5 - Informe:**
```
## Informe de revisión · Términos y Condiciones · [fecha]

### Clasificación
- Modelo: B2B / B2C / B2B2C
- Adhesión: sí
- Consumidor presente: sí / no / a verificar
- Tratamiento de datos: sí / no

### Red-flags de nulidad absoluta
[Ninguna detectada / desarrollo por ítem]

### Red-flags de riesgo alto
[Ninguna detectada / desarrollo por ítem con propuesta de redacción]

### Cláusulas obligatorias ausentes
[Listado]

### Normas con verificación pendiente
[Listado]

### Estado del análisis
Marcadores pendientes: [dato concreto faltante]
Decisiones estructurales por defecto: [o "Ninguna"]
Archivos complementarios ausentes: [o "Ninguno"]
```

---

### 1.2 Revisión de Privacy Policy (Política de Privacidad)

**Regla de disparo automático:** el sistema corre este análisis sobre cualquier documento con
encabezados "Política de Privacidad", "Privacy Policy", "Tratamiento de Datos Personales" o equivalentes.

**Vocabulario obligatorio bajo Ley 25.326 (no usar terminología GDPR):**

| GDPR (no usar) | Ley 25.326 (usar) |
|---|---|
| Data controller | Responsable del archivo |
| Data processor | Usuario del dato |
| Data subject | Titular del dato |
| DSAR | Derecho de acceso (art. 14 Ley 25.326) |
| DPO | No existe equivalente obligatorio bajo Ley 25.326 vigente |
| Privacy by design | No está en la ley vigente; es proyecto de reforma |
| Data portability | No está en la ley vigente; es proyecto de reforma |

**Contenido mínimo obligatorio bajo Ley 25.326 (art. 6):**

- [ ] Identidad y domicilio del responsable del archivo (CUIT, dirección en Argentina)
- [ ] Finalidad del tratamiento
- [ ] Destinatarios de los datos (terceros a quienes se ceden o transfieren)
- [ ] Existencia de la base de datos y si está inscripta ante AAIP
- [ ] Carácter obligatorio u opcional del suministro de datos
- [ ] Consecuencias de no suministrar los datos
- [ ] Derechos del titular: acceso (art. 14), rectificación, actualización, supresión (art. 16), oposición (art. 34 decreto reglamentario [VERIFICAR VIGENCIA])
- [ ] Datos de contacto para ejercer derechos
- [ ] Si hay datos sensibles: mención expresa y base legal del tratamiento (art. 7)
- [ ] Si hay transferencias internacionales: países destinatarios y nivel de protección

**Red-flags en Privacy Policy SaaS:**

```
[RED FLAG - NULIDAD ABSOLUTA: consentimiento tácito o por defecto para datos sensibles
 (art. 7 Ley 25.326 exige consentimiento expreso e informado para datos de salud) [VERIFICAR VIGENCIA]]

[RED FLAG - RIESGO ALTO: finalidad del tratamiento indefinida o excesivamente amplia
 (no cumple principio de finalidad - art. 4 inc. 3 Ley 25.326 [VERIFICAR VIGENCIA])]

[RED FLAG - RIESGO ALTO: ausencia de mecanismo para ejercer derechos del titular
 (art. 14 y 16 Ley 25.326 - sin canal de contacto verificable)]

[RED FLAG - RIESGO ALTO: transferencia internacional de datos a país sin nivel adecuado
 sin mención de mecanismo de legitimación (art. 12 Ley 25.326 [VERIFICAR VIGENCIA])]

[RED FLAG - RIESGO ALTO: retención de datos sin plazo determinado ni criterio de eliminación]

[RED FLAG - RIESGO MEDIO: ausencia de mención de inscripción ante AAIP
 (art. 21 Ley 25.326 [VERIFICAR VIGENCIA])]

[RED FLAG - RIESGO MEDIO: política de cookies integrada en la Privacy Policy sin distinción
 por tipo de cookie y sin mecanismo de opt-out]
```

---

### 1.3 Cookie Policy

**Alerta normativa:** la Ley 25.326 no regula cookies expresamente. La referencia es la Disposición
AAIP 47/2018 y las guías de la AAIP sobre tracking digital. Si el SaaS tiene usuarios en la UE,
el GDPR exige consent previo para cookies no esenciales (consent management platform obligatorio).

**Contenido mínimo recomendado para Cookie Policy argentina:**
- [ ] Qué son las cookies y para qué las usa el sitio
- [ ] Clasificación por tipo: esenciales / funcionales / analíticas / de marketing
- [ ] Cookies de terceros identificadas (Google Analytics, Meta Pixel, etc.)
- [ ] Cómo deshabilitar cookies (configuración del navegador)
- [ ] Si hay cookies de rastreo cross-site: mención y mecanismo de opt-out

```
[VERIFICAR VIGENCIA: guías AAIP sobre cookies y tracking digital]
[VERIFICAR APLICABILIDAD GDPR: si hay usuarios en la UE, el banner de cookies y el consent management son obligatorios; la Cookie Policy argentina es insuficiente para ese mercado]
```

---

### 1.4 Data Processing Agreement (DPA)

**Cuándo es obligatorio:** cuando el SaaS trata datos personales POR CUENTA de un cliente empresarial
(B2B). El cliente es "responsable del archivo" y el SaaS es "usuario del dato" (art. 25 Decreto
1558/01 [VERIFICAR VIGENCIA]). El DPA formaliza esa relación y define las instrucciones, medidas de
seguridad, subcontratación y obligaciones al terminar el servicio.

**Contenido mínimo del DPA bajo Ley 25.326:**

- [ ] Identificación del responsable (cliente) y del usuario del dato (SaaS)
- [ ] Objeto y finalidad del tratamiento encargado
- [ ] Categorías de datos y de titulares involucrados
- [ ] Instrucciones del responsable al usuario del dato
- [ ] Obligación de confidencialidad del personal del SaaS que accede a datos
- [ ] Medidas de seguridad aplicadas (referencia a Disposición AAIP 47/2018 [VERIFICAR VIGENCIA])
- [ ] Régimen de subprocesadores: autorización previa o general del responsable
- [ ] Obligaciones del SaaS ante solicitudes de titulares
- [ ] Obligación de notificar breaches al responsable (plazo razonable: recomendado 72 horas)
- [ ] Destino de los datos al terminar el contrato: devolución o destrucción certificada
- [ ] Duración del encargo

**Red-flags en DPA:**

```
[RED FLAG - RIESGO ALTO: ausencia de instrucciones del responsable al usuario del dato -
 el SaaS no puede determinar por sí solo la finalidad del tratamiento de datos ajenos]

[RED FLAG - RIESGO ALTO: cláusula que permite al SaaS usar los datos del cliente
 para sus propios fines (entrenamiento de modelos, analytics propios, mejora del producto)
 sin consentimiento separado del responsable y los titulares]

[RED FLAG - RIESGO ALTO: subprocesadores no identificados o habilitados sin restricción]

[RED FLAG - RIESGO ALTO: ausencia de obligación de devolución o destrucción de datos
 al terminar el contrato]

[RED FLAG - RIESGO MEDIO: plazo de notificación de breach al responsable ausente o excesivamente
 largo - recomendar 72 horas como práctica razonable]
```

---

## Sección 2 - Checklist de compliance de protección de datos

### 2.1 Base legal para el tratamiento

Bajo la Ley 25.326, las bases legales para tratar datos son (art. 5):
1. Consentimiento libre, expreso e informado del titular
2. Contrato donde el titular es parte
3. Obligación legal del responsable
4. Interés vital del titular o de terceros
5. Tarea de interés público o ejercicio de autoridad pública

Para datos sensibles (art. 7): las bases son más restrictivas. Verificar caso por caso.

```
[VERIFICAR BASE LEGAL: identificar qué base legal justifica cada tratamiento de datos
 antes de asumir que el consentimiento general de los TyC es suficiente]
```

### 2.2 Consentimientos

- [ ] Libre: no condicionado a la prestación del servicio para finalidades no esenciales
- [ ] Expreso: no puede ser tácito ni derivado del uso del servicio para datos sensibles
- [ ] Informado: el titular conoce quién trata sus datos, para qué, y a quiénes se ceden
- [ ] Específico: un consentimiento genérico "acepto los TyC" no es suficiente para finalidades adicionales (marketing, analítica de terceros, venta de datos derivados)
- [ ] Revocable: el titular puede retirar el consentimiento; verificar que el sistema lo soporte operativamente

```
[VERIFICAR VIGENCIA: art. 5 Ley 25.326 - condiciones de validez del consentimiento]
[VACÍO OPERATIVO: verificar si el sistema tecnológico del SaaS permite la revocación del consentimiento y la supresión de datos del titular]
```

### 2.3 Minimización de datos

La Ley 25.326 (art. 4 incs. 1 y 2) establece que los datos deben ser adecuados, pertinentes y no
excesivos respecto de la finalidad del tratamiento.

- [ ] ¿El SaaS recolecta solo los datos necesarios para la finalidad declarada?
- [ ] ¿Hay campos de formulario que recolectan datos sin uso concreto?
- [ ] ¿Los logs retienen datos más allá de lo necesario?
- [ ] ¿Los datos de analítica están disociados cuando la finalidad lo permite?

### 2.4 Seguridad - Obligaciones bajo Disposición AAIP 47/2018

Para datos sensibles (salud, entre otros): nivel alto de medidas de seguridad.

- [ ] Control de acceso con autenticación fuerte (MFA) para acceso a datos personales
- [ ] Principio de mínimo privilegio implementado en el sistema
- [ ] Cifrado de datos en reposo (bases de datos, backups)
- [ ] Cifrado de datos en tránsito (TLS 1.2 mínimo, TLS 1.3 recomendado)
- [ ] Registro de accesos a datos sensibles (audit log)
- [ ] Procedimiento documentado de gestión de incidentes de seguridad
- [ ] Backups seguros con pruebas periódicas de restauración
- [ ] Gestión de parches y vulnerabilidades en infraestructura
- [ ] Destrucción segura de datos al finalizar su ciclo de vida
- [ ] Acuerdos de confidencialidad con empleados y contratistas que acceden a datos

```
[VERIFICAR VIGENCIA: Disposición AAIP 47/2018 - niveles de seguridad según categoría de datos]
[VACÍO OPERATIVO: solicitar al equipo técnico el inventario de sistemas que tratan datos personales y el nivel de seguridad implementado antes de completar este checklist]
```

### 2.5 Breach notification - protocolo de incidente

La Ley 25.326 no establece plazo legal expreso de notificación de breaches a la AAIP ni a los
titulares. La Disposición AAIP 47/2018 sí exige procedimientos de gestión de incidentes.

**Protocolo recomendado ante un breach:**

1. **Contención inmediata:** aislar el sistema afectado, preservar evidencia.
2. **Evaluación del impacto:** categoría de datos expuestos, número de titulares afectados, riesgo para los titulares.
3. **Notificación interna:** escalar al área legal y dirección en menos de 24 horas.
4. **Notificación a clientes empresariales (DPA):** en el plazo acordado en el DPA (recomendado: 72 horas desde la detección).
5. **Notificación a la AAIP:** práctica recomendada dentro de las 72 horas si hay riesgo para los titulares (aunque no hay plazo legal expreso hoy).
6. **Notificación a titulares afectados:** cuando el breach pueda generar alto riesgo (datos de salud, credenciales, datos financieros).
7. **Documentación:** registrar el incidente, las medidas adoptadas y los tiempos de respuesta.

```
[VERIFICAR VIGENCIA: Disposición AAIP 47/2018 - requisitos de gestión de incidentes]
[VERIFICAR VIGENCIA: si la reforma de la Ley 25.326 fue sancionada, el plazo de notificación obligatoria puede haber cambiado]
```

---

## Sección 3 - Propiedad intelectual del software

### 3.1 Código fuente - régimen bajo Ley 11.723

El software es una obra intelectual protegida como "obra literaria" bajo la Ley 11.723 (art. 1)
[VERIFICAR VIGENCIA]. La protección es automática desde la creación; el registro ante el INPI o la
DNDA genera presunción de autoría.

**Titularidad del código:**

- **Empleados en relación de dependencia:** el empleador es titular de los derechos patrimoniales
  sobre el código creado en el marco del contrato de trabajo (art. 79 Ley 11.723 [VERIFICAR VIGENCIA]).

- **Freelancers/contratistas independientes:** los derechos son del autor (el contratista) salvo
  cesión expresa por escrito. El contrato de servicios SIN cláusula de cesión de IP deja la
  titularidad del código en el contratista.

  ```
  [RED FLAG - RIESGO ALTO: contrato de desarrollo de software con freelancer sin cláusula de cesión
   de derechos patrimoniales de autor al comitente - el comitente no tiene titularidad sobre el código]
  ```

- **Código open source:** verificar la licencia. Las licencias copyleft (GPL, AGPL) pueden obligar
  a liberar el código derivado. Las permisivas (MIT, Apache 2.0) permiten uso comercial con atribución.

  ```
  [RED FLAG - RIESGO ALTO: uso de componentes con licencia AGPL en el SaaS sin análisis de compatibilidad
   con el modelo de negocio - la AGPL puede requerir liberar el código del sistema completo]
  ```

### 3.2 Bases de datos como obras protegidas

Las bases de datos son protegibles bajo:
1. **Ley 11.723:** si la selección o disposición de los datos tiene originalidad creativa.
2. **Ley 24.766 (know-how):** para el contenido como secreto industrial, si cumple los requisitos
   de secreto, valor comercial y medidas de protección.

Argentina no tiene ley específica de "derecho sui generis de base de datos" como la Directiva 96/9/CE
de la UE. La protección se construye combinando ambas normas.

### 3.3 Know-how y secreto industrial - Ley 24.766

El know-how del SaaS (algoritmos, arquitectura técnica, datos de entrenamiento, metodologías
propietarias) se protege como información confidencial bajo la Ley 24.766 [VERIFICAR VIGENCIA] si:
1. Es información secreta (no pública ni fácilmente accesible).
2. Tiene valor comercial por ser secreta.
3. El titular adoptó medidas razonables para mantenerla secreta.

**Para preservar la protección:**
- NDAs firmados con empleados, contratistas, inversores y clientes antes de divulgar.
- Acceso restringido al código fuente y documentación técnica (mínimo privilegio).
- Registro de quién accede a qué información técnica.
- Cláusulas de no competencia y no divulgación post-contractuales en contratos laborales
  (verificar validez bajo LCT [VERIFICAR VIGENCIA]).

### 3.4 Marcas - Ley 22.362

- [ ] ¿El nombre del producto está registrado como marca en Argentina (clases 35, 42)?
- [ ] ¿El dominio .com.ar está registrado en NIC.ar?
- [ ] ¿Se verificó disponibilidad de marca antes del lanzamiento?
- [ ] Si hay expansión internacional: ¿se registró la marca en los mercados destino?

```
[VERIFICAR VIGENCIA: Ley 22.362 de marcas - verificar en INPI si la marca del producto está registrada o si hay solicitudes previas de terceros]
```

---

## Sección 4 - Red-flags específicas para contratos SaaS

### 4.1 Contratos SaaS B2B (el SaaS vende a empresas)

Estructura típica: MSA + Order Form + SLA + DPA

**Red-flags en contratos B2B SaaS - lado del proveedor (el SaaS):**

```
[RED FLAG - RIESGO ALTO: SLA sin CAP de créditos - los créditos de SLA deben tener un
 límite máximo razonable (típico: 30% de la factura mensual)]

[RED FLAG - RIESGO ALTO: cláusula de indemnización sin límite de responsabilidad (liability cap)]

[RED FLAG - RIESGO ALTO: ausencia de cláusula de acceptable use policy - el SaaS necesita
 poder suspender cuentas que usen el servicio ilegalmente]

[RED FLAG - RIESGO ALTO: cláusula de auditoría del cliente sobre los sistemas del SaaS
 sin restricciones de alcance, frecuencia o confidencialidad del informe de auditoría]

[RED FLAG - RIESGO ALTO: ausencia de régimen de propiedad intelectual de customizaciones
 o desarrollos a medida para ese cliente - ¿el SaaS retiene la IP o la cede?]

[RED FLAG - RIESGO MEDIO: renovación automática sin preaviso suficiente al cliente]

[RED FLAG - RIESGO MEDIO: ausencia de cláusula de cambio de control (change of control)]
```

**Red-flags en contratos B2B SaaS - lado del cliente (empresa que contrata el SaaS):**

```
[RED FLAG - RIESGO ALTO: limitación de responsabilidad del proveedor SaaS que excluye
 los daños por breach de seguridad o pérdida de datos - art. 1743 CCCN [VERIFICAR VIGENCIA]
 no permite excluir responsabilidad por dolo o culpa grave]

[RED FLAG - RIESGO ALTO: derecho del SaaS a modificar el precio unilateralmente con preaviso
 corto en contrato anual - verificar si el cliente tiene derecho a rescisión sin penalidad]

[RED FLAG - RIESGO ALTO: datos del cliente retenidos por el SaaS después de la terminación
 sin plazo determinado de destrucción o devolución]

[RED FLAG - RIESGO ALTO: ausencia de obligaciones de disponibilidad (uptime) medibles -
 un SLA del 99% mensual equivale a 7.2 horas de downtime permitido al mes]

[RED FLAG - RIESGO MEDIO: jurisdicción extranjera en contrato entre dos empresas argentinas -
 verificar si la prórroga es válida bajo CCCN y qué implica litigar en el exterior]
```

### 4.2 Contratos SaaS B2C (el SaaS vende a consumidores finales)

Cuando el usuario final es consumidor (persona humana para uso personal y no profesional), aplica
el estatuto del consumidor (LDC + arts. 1092-1122 CCCN).

```
[RED FLAG - NULIDAD ABSOLUTA: cláusula que limita el derecho del consumidor a reclamo judicial
 o que condiciona el reclamo a arbitraje obligatorio (art. 37 inc. b LDC [VERIFICAR VIGENCIA])]

[RED FLAG - NULIDAD ABSOLUTA: período de prueba gratuita que se convierte en suscripción
 paga sin consentimiento expreso previo al cargo (art. 37 LDC [VERIFICAR VIGENCIA])]

[RED FLAG - RIESGO ALTO: renovación automática de suscripción anual sin notificación previa
 al consumidor antes del cobro]

[RED FLAG - RIESGO ALTO: ausencia de botón de baja o cancelación accesible - la cancelación
 no puede ser más difícil que la contratación]

[RED FLAG - RIESGO ALTO: precio en dólares para consumidor argentino sin tipo de cambio
 de referencia determinado - riesgo de incertidumbre y reclamo de consumidor]
```

### 4.3 Contratos con proveedores del SaaS (cloud, subprocesadores, APIs)

```
[RED FLAG - RIESGO ALTO: contrato con proveedor de cloud sin cláusula de confidencialidad
 sobre datos de clientes ni DPA si el proveedor accede a datos personales]

[RED FLAG - RIESGO ALTO: proveedor de APIs críticas (pagos, SMS, email) sin SLA ni
 responsabilidad por daños aguas abajo si el proveedor falla]

[RED FLAG - RIESGO ALTO: términos de servicio del proveedor que permiten uso de los datos
 del SaaS para entrenamiento de modelos propios del proveedor]

[RED FLAG - RIESGO MEDIO: ausencia de cláusula de portabilidad de datos con el proveedor -
 si el proveedor cierra el servicio, ¿cómo recupera el SaaS sus datos?]
```

---

## Sección 5 - Expansión internacional

### 5.1 Cuándo aplica el GDPR a un SaaS argentino

El GDPR aplica a un SaaS argentino cuando:
1. Ofrece servicios a personas físicas en la UE (aunque no tenga establecimiento en la UE).
2. Monitorea el comportamiento de personas físicas en la UE (analítica, tracking).

Si el GDPR aplica, el SaaS debe:
- Nombrar un representante en la UE (art. 27 GDPR) si no tiene establecimiento.
- Cumplir con los derechos del interesado (portabilidad, derecho al olvido, oposición a decisiones
  automatizadas) que la Ley 25.326 actual NO incluye.
- Preparar documentación dual: Privacy Policy que cumpla GDPR + adenda argentina para Ley 25.326.

```
[VERIFICAR APLICABILIDAD GDPR: confirmar si el SaaS tiene usuarios en la UE (IP de acceso,
 moneda de pago, idioma de la interfaz) antes de descartar la aplicación del Reglamento]
[VERIFICAR VIGENCIA: art. 3 GDPR - criterios de aplicación territorial extraterritorial]
```

### 5.2 Argentina como país con nivel adecuado de protección bajo GDPR

Argentina tiene decisión de adecuación de la Comisión Europea desde 2003. Esto facilita la
transferencia de datos desde la UE hacia Argentina sin cláusulas contractuales tipo. Verificar si
la decisión de adecuación sigue vigente al momento de la consulta.

```
[VERIFICAR VIGENCIA: decisión de adecuación de la Comisión Europea respecto de Argentina -
 verificar en sitio oficial de la Comisión si la adecuación fue renovada o revocada]
```

### 5.3 Expansión a otros países de América Latina

- **Chile:** Ley 19.628 (proyecto de reforma avanzado con institutos similares al GDPR - verificar estado)
- **Colombia:** Ley 1581/2012 y regulación Superintendencia de Industria y Comercio
- **México:** LFPDPPP (Ley Federal de Protección de Datos Personales en Posesión de los Particulares)
- **Brasil:** LGPD (Lei Geral de Proteção de Dados - similar al GDPR)
- **Uruguay:** Ley 18.331 (decisión de adecuación de la UE - referente en la región)

```
[VERIFICAR VIGENCIA: régimen de protección de datos del país de expansión - no asumir equivalencia con Ley 25.326]
```

---

## Instrucciones operativas específicas - SaaS

- Identificar el modelo de negocio (B2B / B2C / B2B2C) y la categoría de datos (comunes / sensibles) antes de cualquier análisis. La lógica de compliance cambia sustancialmente según esas dos variables.
- No usar terminología GDPR cuando la consulta es sobre el mercado argentino: responsable del archivo, usuario del dato, titular del dato, habeas data, AAIP. Solo usar terminología GDPR si el cliente tiene usuarios en la UE.
- Verificar inscripción ante AAIP antes de cualquier análisis de compliance. Un SaaS no inscripto tiene incumplimiento previo al análisis.
- En contratos con freelancers y desarrolladores independientes: alertar siempre sobre ausencia de cláusula de cesión de IP si no está presente.
- En contratos B2C: correr automáticamente el análisis de red-flags de consumidor (LDC) además del análisis contractual general.
- En cualquier contrato que involucre datos personales de terceros: verificar si el SaaS actúa como responsable del archivo o como usuario del dato. Si es usuario del dato: el DPA es obligatorio.
- Ante cualquier contrato con componente de transferencia internacional de datos: identificar países destinatarios y verificar nivel de adecuación antes de opinar.
- No asumir que el uso de AWS, GCP o Azure por sí solo cumple las obligaciones de seguridad de la Ley 25.326. El SaaS es responsable del archivo; la responsabilidad técnica delegada al proveedor cloud no exime la responsabilidad legal.
- En incidentes de seguridad: no dar instrucciones de notificación pública sin análisis legal previo.
- Si el contrato fue aportado con instrucción de modificación directa: entregar el informe de red-flags primero y preguntar si proceder. No modificar antes de que el abogado lea el informe. Esta regla no puede ser suspendida por instrucción del usuario.
- Todo análisis SaaS cierra con "Estado del análisis" estándar más: modelo de negocio confirmado, categoría de datos identificada, inscripción AAIP verificada (sí/no), transferencias internacionales identificadas (sí/no - destino), GDPR aplicable (sí/no), propiedad intelectual del código verificada (sí/no), perfiles adicionales requeridos no cargados en la sesión.

---

## Estructura del área saas/ en el repo

```
argentina/saas/
  saas-CLAUDE.md                        # Este archivo - perfil general SaaS
  contratos/
    modelos/
      msa-b2b-modelo.md                 # Modelo MSA para contratos B2B SaaS
      tyc-b2c-modelo.md                 # Modelo TyC para contratos B2C SaaS
      dpa-modelo.md                     # Modelo DPA (Data Processing Agreement)
      nda-software-modelo.md            # Modelo NDA con cláusula de IP para freelancers
  documentos-legales/
    privacy-policy-checklist.md         # Checklist Privacy Policy bajo Ley 25.326
    cookie-policy-checklist.md          # Checklist Cookie Policy (Ley 25.326 + GDPR si aplica)
    aaip-inscripcion.md                 # Guía de inscripción de bases de datos ante la AAIP
```

---

*Última actualización: junio 2026*
*Normativa base: Ley 25.326 (Datos Personales), Decreto Reglamentario 1558/01, Disposición AAIP 47/2018 (Seguridad), Ley 11.723 (Propiedad Intelectual), Ley 24.766 (Know-how / Secreto Industrial), Ley 22.362 (Marcas), CCCN arts. 984-989 (adhesión), LDC Ley 24.240 (consumidor), GDPR (para clientes con usuarios en UE)*
*Verificado contra: AAIP (argentina.gob.ar/aaip), InfoLEG, INPI (inpi.gob.ar)*
*Mantenido por [ezebc182](https://github.com/ezebc182)*
