# Auditoría interna de cumplimiento — SaaS argentino

> Marco normativo: Disposición AAIP 47/2018 [VERIFICAR VIGENCIA: verificar si fue reemplazada o modificada antes de ejecutar esta auditoría], Ley 25.326 [VERIFICAR VIGENCIA].

> Uso: ejecutar esta auditoría al menos una vez al año, o cada vez que se incorporen nuevos tipos de datos personales, nuevos proveedores cloud, o se produzcan cambios significativos en la arquitectura del sistema. El resultado documentado sirve como evidencia de cumplimiento ante una inspección de la AAIP.

Registrá la fecha de la auditoría, quién la realizó, y el estado de cada ítem (cumplido / no cumplido / en progreso con fecha estimada).

---

## 1. Inventario de datos personales

**Objetivo**: saber exactamente qué datos personales trata el SaaS, dónde están y quién tiene acceso. Sin este mapa, cualquier evaluación de riesgo es especulación.

- [ ] **Mapa de datos completo**: documento o herramienta que liste:
  - Qué datos personales se recolectan (campos por formulario, datos generados automáticamente)
  - Dónde se almacenan (base de datos principal, backups, logs, S3/storage, herramientas de terceros)
  - Quién tiene acceso (por rol: desarrollador, soporte, administrador, automatizaciones)
  - Con qué finalidad se usa cada dato
  - Por cuánto tiempo se retiene

- [ ] **Clasificación por categoría de sensibilidad**:
  - Datos comunes: nombre, email, teléfono, dirección, historial de uso del producto
  - Datos sensibles bajo art. 2 Ley 25.326 [VERIFICAR VIGENCIA]: datos de salud, ideología política, vida sexual, origen racial, convicciones religiosas, antecedentes penales
  - [RED FLAG] Si el SaaS trata datos sensibles sin saberlo explícitamente (ej.: un SaaS de turnos médicos que almacena el motivo de la consulta), es el momento de identificarlo y asegurarse de que el nivel de seguridad implementado corresponde

- [ ] **Inventario de bases de datos inscriptas ante la AAIP vs. bases que existen en el sistema**:
  - Listar todas las bases registradas ante la AAIP con su número de registro
  - Listar todas las bases de datos reales que contienen datos personales
  - [RED FLAG] Si hay bases que existen en el sistema pero no están inscriptas, es una infracción a art. 21 Ley 25.326 [VERIFICAR VIGENCIA] — inscribir antes de continuar

- [ ] **Flujos de datos documentados**:
  - De dónde vienen los datos: formulario de registro, importación por el cliente, API de terceros, generación automática por el sistema
  - A dónde van: base de datos propia, herramientas de terceros, clientes empresariales, usuarios finales
  - Qué terceros procesan los datos (ver sección 4 — Contratos y acuerdos)

---

## 2. Control de acceso

**Objetivo**: que solo accedan a los datos personales quienes tienen una razón legítima y documentada.

- [ ] **Autenticación fuerte (MFA) para acceso administrativo**:
  - MFA habilitado y obligatorio para: acceso a bases de datos de producción, consola de administración del cloud provider, herramientas de soporte que muestran datos de usuarios, repositorios con acceso a secrets de producción
  - [RED FLAG] Credenciales de producción sin MFA son la causa más común de brechas evitables

- [ ] **Principio de mínimo privilegio implementado**:
  - Cada empleado accede solo a los datos que necesita para su función específica
  - El desarrollador de frontend no necesita acceso directo a la base de datos de producción
  - El agente de soporte no necesita ver contraseñas ni información de pago
  - Documentar el esquema de permisos por rol

- [ ] **Proceso documentado de alta y baja de accesos**:
  - Onboarding: checklist de accesos a otorgar según rol, con aprobación del responsable
  - Offboarding: checklist de accesos a revocar el día que la persona deja la empresa — no la semana siguiente
  - [RED FLAG] Cuentas activas de ex-empleados con acceso a sistemas de producción son un riesgo de seguridad y un incumplimiento de la Disposición 47/2018 [VERIFICAR VIGENCIA]

- [ ] **Registro de accesos a datos sensibles (audit log)**:
  - Si el SaaS trata datos de salud u otros datos sensibles: implementar audit log de quién accedió a qué registro, cuándo, desde qué IP
  - Período de retención del audit log: definirlo explícitamente (recomendado: mínimo 12 meses, verificar si hay requisito normativo específico para el sector)
  - El audit log debe ser inmutable: los mismos que tienen acceso a los datos no deben poder borrar los registros del audit log

---

## 3. Seguridad técnica

**Objetivo**: verificar que las medidas técnicas implementadas corresponden al nivel requerido por la Disposición AAIP 47/2018 [VERIFICAR VIGENCIA] para las categorías de datos tratadas.

- [ ] **Cifrado de datos en reposo**:
  - Bases de datos con datos personales: cifrado a nivel de disco habilitado (AWS RDS encryption, GCP Cloud SQL encryption, o equivalente del cloud provider usado)
  - Backups: también cifrados — verificar que la configuración del backup hereda el cifrado de la base de datos o tiene cifrado propio
  - Datos sensibles (salud, etc.): considerar cifrado a nivel de campo además del cifrado de disco, con gestión de claves separada de los datos

- [ ] **Cifrado TLS para datos en tránsito**:
  - TLS 1.2 mínimo en todos los endpoints (TLS 1.3 recomendado)
  - Verificar con herramienta externa: ssllabs.com/ssltest o equivalente
  - [RED FLAG] Calificación C o menor en SSL Labs indica configuración TLS deficiente — corregir antes de continuar

- [ ] **Gestión de parches de infraestructura**:
  - Sistema operativo: actualizaciones de seguridad aplicadas con frecuencia definida (recomendado: automáticas para parches críticos)
  - Dependencias del runtime (Node.js, Python, Go, etc.): proceso de actualización ante CVE críticos
  - Dependencias de aplicación (npm, pip, etc.): verificar con herramienta de análisis de vulnerabilidades (Dependabot, Snyk, o equivalente)
  - Documentar el proceso: "quién es responsable", "cuál es el plazo máximo para parches críticos"

- [ ] **Proceso de gestión de vulnerabilidades documentado**:
  - ¿Cómo se enteran de nuevas vulnerabilidades que afectan al stack? (suscripción a advisories del proveedor, GitHub Dependabot, etc.)
  - ¿Cuál es el criterio de priorización? (CVSS score, si hay exploit público, si afecta datos personales)
  - ¿Cuáles son los SLAs internos de remediación por criticidad?

- [ ] **Backups seguros con pruebas de restauración**:
  - Backups de bases de datos: frecuencia, retención, ubicación (idealmente fuera de la misma región que producción)
  - [RED FLAG] Tener backups que nunca se probaron es equivalente a no tener backups — una restauración exitosa debe validarse periódicamente (recomendado: al menos una vez cada 6 meses)
  - Tiempo de recuperación: ¿cuánto tarda restaurar desde backup? ¿lo saben? ¿está documentado?

---

## 4. Contratos y acuerdos

**Objetivo**: verificar que las obligaciones legales de protección de datos están formalizadas con todos los actores que acceden a datos personales.

- [ ] **DPA firmado con cada proveedor que accede a datos personales**:
  - Cloud providers (AWS, GCP, Azure, DigitalOcean, etc.): verificar si el acuerdo de servicios incluye cláusulas de procesamiento de datos o si hay DPA separado
  - Plataformas de email transaccional (SendGrid, Resend, Postmark, AWS SES): verificar DPA
  - Herramientas de soporte al cliente (Intercom, Zendesk, Freshdesk, Crisp): verificar DPA — estas herramientas ven datos de usuarios directamente
  - Herramientas de monitoreo y observabilidad (Datadog, Sentry, New Relic): verificar qué datos personales ingieren y si hay DPA
  - [RED FLAG] Proveedor con acceso a datos personales sin DPA: el SaaS es potencialmente responsable solidario ante incidentes del proveedor

- [ ] **NDA firmado con empleados y contratistas que acceden a datos personales**:
  - Empleados en relación de dependencia: la obligación de confidencialidad debe estar en el contrato de trabajo o en acuerdo separado
  - Contratistas externos (freelancers, agencias, consultores): NDA firmado antes de tener acceso a cualquier sistema o dato de producción
  - El NDA debe incluir obligación de confidencialidad específica sobre datos personales de usuarios, no solo sobre información comercial genérica

- [ ] **Cláusulas de confidencialidad en contratos del área técnica**:
  - Verificar que los contratos del área técnica (incluyendo roles que no son "desarrolladores" pero acceden a sistemas con datos: soporte técnico, DevOps, QA) incluyen obligación de confidencialidad

---

## 5. Procedimientos documentados

**Objetivo**: verificar que los procesos críticos están escritos, no solo en la cabeza de una persona.

- [ ] **Procedimiento de gestión de incidentes de seguridad**:
  - Debe existir como documento escrito (ver `breach-protocol.md` para el modelo)
  - El equipo técnico debe conocerlo ANTES de que ocurra un incidente
  - Incluir: quién decide qué, cadena de escalada, contactos de proveedores de respuesta a incidentes si aplica

- [ ] **Procedimiento para atender solicitudes de titulares**:
  - Derecho de acceso (art. 14 Ley 25.326 [VERIFICAR VIGENCIA]): el titular puede pedir conocer sus datos — ¿quién recibe la solicitud, quién la procesa, cuál es el plazo de respuesta?
  - Derecho de rectificación (art. 16 Ley 25.326 [VERIFICAR VIGENCIA]): ¿cómo se actualiza un dato incorrecto?
  - Derecho de supresión (art. 16 Ley 25.326 [VERIFICAR VIGENCIA]): ¿cómo se borra la cuenta y todos los datos del titular?
  - Documentar los plazos: verificar plazos legales vigentes al momento de implementar
  - [RED FLAG] No tener un proceso para atender solicitudes de supresión ("derecho al olvido") es un incumplimiento frecuente en SaaS — la posibilidad de borrar cuenta no es suficiente si los datos permanecen en backups indefinidamente

- [ ] **Procedimiento de destrucción segura de datos al finalizar su ciclo de vida**:
  - ¿Qué pasa con los datos cuando un cliente cancela su suscripción? ¿Y con los datos de usuarios inactivos?
  - Definir: período de retención post-cancelación, proceso de eliminación o anonimización, confirmación documentada de la eliminación
  - Para backups: los backups también deben entrar en el ciclo de vida — un backup de 2 años puede contener datos que deberían haber sido eliminados hace 18 meses

---

## 6. Datos sensibles (completar solo si el SaaS trata datos sensibles)

**Aplica si**: el SaaS trata datos de salud, ideología política, vida sexual, origen racial, convicciones religiosas, o antecedentes penales de los titulares.

- [ ] **Política documentada de tratamiento de datos sensibles**:
  - Art. 7 Ley 25.326 [VERIFICAR VIGENCIA]: los datos sensibles solo pueden ser tratados cuando hay razones de interés general autorizadas por ley, o con consentimiento expreso y escrito del titular
  - Documentar: qué datos sensibles se tratan, cuál es la base legal para su tratamiento, quién autorizó internamente el tratamiento

- [ ] **Nivel de seguridad ALTO implementado para sistemas que tratan datos de salud**:
  - La Disposición AAIP 47/2018 [VERIFICAR VIGENCIA] establece requerimientos específicos para el nivel ALTO: cifrado de datos tanto en reposo como en tránsito, control de acceso estricto, audit log de accesos, procedimientos de backup con pruebas de restauración documentadas
  - [RED FLAG] Un SaaS de salud que no implementa nivel ALTO está en incumplimiento normativo — y expuesto a sanciones significativamente mayores que el nivel básico

- [ ] **Personal con acceso a datos de salud capacitado y bajo obligación de confidencialidad**:
  - Formación específica sobre el manejo de datos de salud para el personal con acceso
  - Obligación de confidencialidad reforzada en los contratos de ese personal
  - [RED FLAG] El personal de soporte que accede a datos de salud para resolver consultas técnicas también está bajo esta obligación — no solo el personal médico o clínico
