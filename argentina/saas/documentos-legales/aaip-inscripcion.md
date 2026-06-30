# Guía: Inscripción de bases de datos ante la AAIP
## Ley 25.326 art. 21 — Registro Nacional de Bases de Datos

---

> **ADVERTENCIA NORMATIVA**
>
> El art. 21 de la Ley 25.326 establece la obligatoriedad de inscribir los archivos, registros,
> bases o bancos de datos privados ante el Registro Nacional de Bases de Datos que lleva la AAIP
> [VERIFICAR VIGENCIA: Ley 25.326 art. 21 y Decreto 1558/2001].
>
> El procedimiento operativo de la AAIP (pasos, formularios, URLs, plazos) puede cambiar sin
> reforma legal. Los pasos descritos en esta guía corresponden al proceso conocido al momento
> de la redacción. **Verificar el procedimiento vigente en argentina.gob.ar/aaip antes de
> iniciar el trámite.**

---

## Por qué es obligatorio

El art. 21 de la Ley 25.326 establece que los responsables y usuarios de archivos de datos personales de titularidad privada tienen **la obligación de inscribir sus bases de datos en el Registro Nacional de Bases de Datos de la AAIP antes de ponerlas en funcionamiento**.

No se trata de una recomendación. Es un requisito previo al tratamiento de datos personales.

El incumplimiento del deber de inscripción es una infracción sancionable por la AAIP. Las sanciones previstas en el art. 31 de la ley van desde el apercibimiento hasta la clausura o cancelación del archivo o base de datos, y pueden incluir multas [VERIFICAR VIGENCIA: Ley 25.326 art. 31 y tabla de multas actualizada por resoluciones AAIP].

**La Privacy Policy de un SaaS que no menciona el número de inscripción AAIP tiene un problema de cumplimiento en la fuente, no solo en el documento.**

---

## Qué es una "base de datos" a estos efectos

La Ley 25.326 define "archivo, registro, base o banco de datos" como el conjunto organizado de datos personales que sean objeto de tratamiento o procesamiento, electrónico o no, cualquiera que fuere la modalidad de su formación, almacenamiento, organización o acceso (art. 2).

Para un SaaS, esto incluye:

| Conjunto de datos | ¿Es una base de datos bajo la ley? | Obligación de inscripción |
|---|---|---|
| Usuarios registrados en el producto (nombre, email, contraseña hasheada, plan, fecha de registro) | Sí | Sí |
| Leads o prospectos en el CRM (HubSpot, Salesforce, Pipedrive) | Sí | Sí |
| Suscriptores al newsletter o lista de email marketing | Sí | Sí |
| Empleados o colaboradores del SaaS | Sí | Sí |
| Candidatos a puestos de trabajo (base de RR.HH.) | Sí | Sí |
| Logs de auditoría con IPs y emails asociados | Sí (si permiten identificar personas) | Sí |
| Datos anónimos sin posibilidad de reidentificación | No (art. 2 excluye datos sin posibilidad de identificación) | No |

**Regla práctica**: si el SaaS tiene usuarios que se registran con nombre y email, tiene al menos una base de datos obligatoria de inscribir.

---

## Cuántas bases inscribir

Se inscribe **una base por cada conjunto de datos con finalidad distinta**. No alcanza con inscribir "base de usuarios" si también hay una base de candidatos de RR.HH. con finalidad completamente diferente.

Ejemplos de bases típicas en un SaaS:

1. **Usuarios del producto**: personas que se registran y usan la plataforma
2. **Contactos de ventas y marketing**: leads, prospectos, clientes potenciales del CRM
3. **Suscriptores de comunicaciones**: personas que solo dejaron el email para recibir newsletters
4. **Empleados y colaboradores**: personal de la empresa que opera el SaaS
5. **Candidatos de RR.HH.**: personas que aplicaron a puestos de trabajo

Cada una de estas finalidades es distinta → cada una requiere su propia inscripción.

---

## Datos que se declaran en la inscripción

Para cada base de datos, la inscripción ante la AAIP requiere declarar:

| Campo | Descripción |
|---|---|
| Nombre de la base | Nombre descriptivo (ej: "Usuarios de la plataforma Deshoku SaaS") |
| Finalidad del tratamiento | Para qué se usan los datos (específico) |
| Tipo de datos | Datos comunes / datos sensibles |
| Descripción de los datos | Categorías de datos que se tratan (ej: nombre, email, IP, datos de facturación) |
| Cantidad estimada de titulares | Número aproximado de personas cuyos datos se tratan |
| Origen de los datos | Cómo se obtienen (registro directo del usuario, formulario, importación, etc.) |
| Destinatarios de los datos | Terceros a quienes se ceden o transfieren los datos |
| Transferencias internacionales | Si los datos salen del país: países destinatarios |
| Medidas de seguridad | Descripción general de las medidas técnicas y organizativas aplicadas |
| Responsable del archivo | Nombre / razón social, CUIT, domicilio |

---

## Pasos del proceso de inscripción

[VERIFICAR VIGENCIA: el procedimiento descripto puede haber cambiado. Verificar en argentina.gob.ar/aaip antes de iniciar el trámite]

**Paso 1 — Inventario previo (hacer antes de abrir el sitio de la AAIP)**

Completar el checklist pre-inscripción que está al final de este documento. Sin el inventario listo, el formulario online queda a medias.

**Paso 2 — Ingresar al sitio de la AAIP**

Ir a: `https://www.argentina.gob.ar/aaip`

Buscar la sección "Registro Nacional de Bases de Datos" o "Protección de Datos Personales" → "Inscripción de bases de datos privadas".

[VERIFICAR VIGENCIA: la URL exacta del formulario puede cambiar con rediseños del portal]

**Paso 3 — Autenticación**

El ingreso se realiza con CUIT/CUIL a través del sistema de autenticación de la plataforma de trámites a distancia (TAD) del gobierno nacional, o mediante el portal específico de la AAIP según el procedimiento vigente.

[VERIFICAR VIGENCIA: verificar si el trámite está disponible en TAD (tramitesadistancia.gob.ar) o en un sistema propio de la AAIP]

**Paso 4 — Completar el formulario de inscripción**

Por cada base de datos:
- Completar los campos según el inventario pre-inscripción
- Indicar si hay transferencias internacionales de datos (sí/no; si sí, indicar los países)
- Describir las medidas de seguridad aplicadas (no es necesario detallar la arquitectura técnica completa; una descripción general es suficiente)

**Paso 5 — Envío y obtención del comprobante**

Una vez enviado el formulario, la AAIP asigna un número de inscripción. Descargar y guardar el comprobante. Este número debe figurar en la Privacy Policy del SaaS.

**Paso 6 — Renovación anual**

La inscripción tiene vigencia anual y debe renovarse [VERIFICAR VIGENCIA: art. 21 Ley 25.326 y reglamentación; confirmar si la renovación sigue siendo anual o si el plazo cambió]. Agendar un recordatorio con 30 días de anticipación al vencimiento.

---

## Qué hacer si la base ya está operando sin inscripción

Si el SaaS está activo y nunca se inscribieron las bases de datos ante la AAIP, la situación es:

1. **La infracción ya existe**: el incumplimiento del art. 21 es un hecho consumado desde el momento en que la base entró en funcionamiento sin inscripción.

2. **Inscribir de inmediato**: la inscripción retroactiva no elimina la infracción, pero demuestra voluntad de cumplimiento ante un eventual procedimiento sancionatorio iniciado por la AAIP (de oficio o por denuncia de un titular de datos).

3. **No esperar**: el riesgo de que un usuario o competidor denuncie el incumplimiento existe siempre. La AAIP puede iniciar actuaciones de oficio.

4. **Actualizar la Privacy Policy**: una vez obtenido el número de inscripción, actualizar inmediatamente el documento con ese dato.

5. **Consulta con abogado**: si el SaaS lleva mucho tiempo operando sin inscripción y maneja datos sensibles o volúmenes grandes, conviene una consulta legal para evaluar el riesgo y estrategia de remediación.

---

## Checklist pre-inscripción

Completar este checklist antes de iniciar el trámite en el sitio de la AAIP. Tener todos los datos a mano reduce el tiempo del trámite.

### Inventario de bases de datos

- [ ] Lista de todas las bases de datos del SaaS con sus finalidades
- [ ] Para cada base: categorías de datos tratados identificadas (nombre, email, IP, datos de facturación, datos de uso del producto, etc.)
- [ ] Para cada base: cantidad estimada de titulares (puede ser una estimación)
- [ ] Para cada base: origen de los datos (registro propio, formulario web, importación desde CSV, etc.)

### Destinatarios y transferencias

- [ ] Lista de terceros a quienes se ceden o comparten datos (proveedores de email, CRM, soporte, pagos)
- [ ] Identificación de si hay transferencias internacionales de datos (usar los servidores de AWS, GCP, Azure en EE.UU. u otros países configura una transferencia internacional) [VERIFICAR VIGENCIA: Ley 25.326 art. 12]
- [ ] Para las transferencias internacionales: países de destino identificados

### Datos del responsable del archivo

- [ ] Razón social completa del responsable
- [ ] CUIT del responsable
- [ ] Domicilio legal completo (calle, número, ciudad, provincia)
- [ ] Email de contacto para ejercicio de derechos de los titulares
- [ ] Teléfono de contacto (puede ser requerido en el formulario)

### Medidas de seguridad

- [ ] Descripción general de las medidas de seguridad técnicas (encriptación de datos en tránsito y en reposo, control de accesos, backups)
- [ ] Descripción general de las medidas organizativas (políticas internas de acceso, capacitación)

### Documentación previa

- [ ] Privacy Policy del SaaS revisada y lista para agregar el número de inscripción una vez obtenido
- [ ] CUIT del representante legal si el trámite lo hace una persona física en nombre de la persona jurídica

---

## Notas operativas adicionales

**Bases de datos de "usuarios del dato" (proveedores SaaS B2B)**

Si el SaaS actúa como "usuario del dato" respecto de los datos de los clientes de sus propios clientes (ej: un SaaS de RR.HH. que procesa datos de los empleados de sus clientes-empresa), la responsabilidad de inscripción ante la AAIP recae en el "responsable del archivo" (el cliente-empresa), no en el SaaS proveedor. Sin embargo, el contrato B2B debe incluir cláusulas de tratamiento de datos que definan roles y responsabilidades. [VERIFICAR VIGENCIA: art. 25 Ley 25.326 y Decreto 1558/2001 sobre contratos con encargados del tratamiento]

**Cambios en la base de datos inscripta**

Si cambia significativamente la finalidad, los tipos de datos o los destinatarios de una base ya inscripta, se debe actualizar la inscripción ante la AAIP. [VERIFICAR VIGENCIA: procedimiento de actualización en la plataforma AAIP]

**Bases de datos de personas jurídicas**

La Ley 25.326 protege datos de personas físicas identificadas o identificables. Los datos de empresas como tales no están protegidos por la ley, aunque los datos de sus representantes o contactos sí lo están. [VERIFICAR VIGENCIA: art. 1 Ley 25.326 y jurisprudencia administrativa de la AAIP]
