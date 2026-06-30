# Compliance Startup SaaS — Checklist antes de lanzar

> Uso: recorré este checklist ANTES de abrir el producto al público. No reemplaza al abogado, pero asegura que llegues a la reunión con los puntos críticos identificados y no descubras problemas después de tener usuarios reales.

Marco normativo aplicable: Ley 25.326 de Protección de los Datos Personales [VERIFICAR VIGENCIA: proyecto de reforma en trámite al momento de esta versión], Disposición AAIP 47/2018 [VERIFICAR VIGENCIA], Ley 11.723 de Propiedad Intelectual [VERIFICAR VIGENCIA], Ley 24.240 de Defensa del Consumidor (LDC) [VERIFICAR VIGENCIA], CCCN.

---

## Fase 1 — Antes de abrir el producto al público (obligatorio)

- [ ] **Inscripción de la base de datos de usuarios ante la AAIP** (art. 21 Ley 25.326 [VERIFICAR VIGENCIA])
  - Aplica a toda base de datos de personas físicas que sea objeto de tratamiento automatizado
  - Ver guía `aaip-inscripcion.md` para el procedimiento paso a paso
  - [RED FLAG] Operar sin inscripción es infracción pasible de sanción. No lo diferís para "cuando tengamos más usuarios"

- [ ] **Privacy Policy publicada y accesible desde el sitio**
  - Debe estar disponible ANTES de que el primer usuario se registre
  - Link visible desde el footer del sitio y desde el formulario de registro
  - Ver `privacy-policy-checklist.md` para el contenido mínimo obligatorio bajo Ley 25.326

- [ ] **Términos y Condiciones publicados con aceptación activa del usuario**
  - La aceptación debe ser un acto positivo: checkbox marcado, botón "Acepto", etc.
  - [RED FLAG] El solo uso del sitio NO implica aceptación de los TyC bajo LDC y criterio AAIP — necesitás consentimiento expreso
  - Para consumidores (B2C): aplicá art. 10 bis LDC sobre cláusulas abusivas [VERIFICAR VIGENCIA]

- [ ] **Cookie Policy publicada si usás cookies de analítica o marketing**
  - Aplica si usás Google Analytics, Meta Pixel, Hotjar, o similares
  - La cookie policy puede estar integrada dentro de la Privacy Policy o ser un documento separado
  - Incluí descripción de cada categoría de cookie, su finalidad y opciones de opt-out

- [ ] **Mecanismo de ejercicio de derechos del titular habilitado**
  - Obligatorio bajo art. 14 y 16 Ley 25.326 [VERIFICAR VIGENCIA]: derecho de acceso, rectificación, supresión y actualización
  - Mínimo aceptable: email de contacto publicado en la Privacy Policy con indicación de plazo de respuesta (máximo 5 días hábiles para acusar recibo, máximo 15 días hábiles para resolver — verificar plazos vigentes)
  - Mejor práctica: formulario web con número de ticket y confirmación automática

- [ ] **Medidas de seguridad implementadas según categoría de datos**
  - Disposición AAIP 47/2018 [VERIFICAR VIGENCIA] establece niveles básico, medio y alto según el tipo de datos tratados
  - Nivel básico: cualquier dato personal — control de acceso, contraseñas, registro de incidentes
  - Nivel alto: datos de salud, ideología, vida sexual, menores, antecedentes penales — cifrado obligatorio, auditoría de accesos
  - Documentar las medidas implementadas (este documento se presenta si hay una inspección)

---

## Fase 2 — Si el producto es B2B (recibís datos de los usuarios de tus clientes)

- [ ] **DPA (Data Processing Agreement) firmado con cada cliente empresarial**
  - Debe estar firmado ANTES de que el cliente te pase cualquier dato de sus usuarios
  - Ver `dpa-modelo.md` para el contenido mínimo
  - [RED FLAG] Sin DPA firmado, la responsabilidad ante los usuarios finales queda indefinida — exposición legal para vos y para tu cliente

- [ ] **Identificar el rol del SaaS en cada relación comercial**
  - ¿Es tu SaaS el responsable del archivo (define la finalidad del tratamiento) o es un usuario del dato (trata datos por instrucción del cliente)?
  - Esta distinción determina quién responde ante el titular y ante la AAIP
  - En la mayoría de los SaaS B2B: el cliente es responsable, el SaaS es usuario del dato (procesador)

- [ ] **Identificar subprocesadores que acceden a datos del cliente**
  - Listá todos los terceros que procesan datos en nombre del SaaS: cloud provider (AWS, GCP, Azure), email provider (SendGrid, Resend), herramientas de soporte (Intercom, Zendesk), herramientas de monitoreo (Datadog, Sentry)
  - Para cada subprocesador: verificar que tenés DPA o cláusulas contractuales de protección de datos con ellos
  - Informar al cliente la lista de subprocesadores en el DPA y actualizarla si incorporás nuevos

---

## Fase 3 — Propiedad intelectual del software

- [ ] **Contratos de desarrolladores en relación de dependencia**
  - Art. 79 Ley 11.723 [VERIFICAR VIGENCIA]: el empleador es titular del software creado en el marco de la relación laboral
  - Verificar que el contrato de trabajo tenga descripción de funciones que incluya el desarrollo de software
  - [RED FLAG] Si el desarrollador fue contratado como "asistente administrativo" y escribió código, la titularidad puede estar en disputa

- [ ] **Contratos de freelancers y contratistas: NDA con cláusula de cesión de IP**
  - Sin cesión expresa de derechos: el contratista retiene los derechos patrimoniales sobre el código que escribió (art. 71 y ss. Ley 11.723 [VERIFICAR VIGENCIA])
  - El NDA debe firmarse ANTES de empezar el trabajo, no al terminarlo
  - Ver `nda-software-modelo.md` para el modelo con cláusula de cesión
  - [RED FLAG] "Le pagué entonces es mío" NO es válido legalmente sin cesión expresa — el pago retribuye el servicio, no transfiere la titularidad intelectual

- [ ] **Inventario de librerías open source y verificación de licencias**
  - Corrés un `npm ls`, `pip list`, o equivalente y revisás las licencias de las dependencias directas e indirectas
  - [RED FLAG] Licencias AGPL v3: si distribuís el software o lo ofrecés como SaaS y usás una librería AGPL, podés estar obligado a publicar tu código fuente completo — ver sección 3.1 de `saas-CLAUDE.md` para el análisis detallado
  - Licencias permisivas (MIT, Apache 2.0, BSD): sin restricciones significativas para SaaS
  - Licencias copyleft débil (LGPL, MPL): revisar caso por caso

- [ ] **Marca comercial: verificación de disponibilidad y registro**
  - Verificar disponibilidad en INPI (www.inpi.gob.ar) en clases 35 (servicios comerciales/SaaS) y 42 (servicios tecnológicos/software)
  - Ley 22.362 [VERIFICAR VIGENCIA]: en Argentina el sistema es "primero que registra" (no "primero que usa")
  - [RED FLAG] Operar años con una marca sin registrar y que otra empresa la registre antes es un riesgo real y costoso de resolver

---

## Fase 4 — Si hay transferencias internacionales de datos (usás AWS, GCP, Azure, Stripe, etc.)

- [ ] **Identificar qué datos personales de usuarios argentinos se procesan fuera de Argentina**
  - La mayoría de los SaaS modernos transfieren datos a servidores en EE.UU. o Europa por defecto
  - Incluir: datos almacenados en la cloud (base de datos, storage), datos procesados por servicios de email, datos enviados a herramientas de analítica y monitoreo

- [ ] **Verificar si el país destinatario tiene nivel adecuado de protección reconocido por Argentina**
  - Art. 12 Ley 25.326 [VERIFICAR VIGENCIA]: la transferencia internacional requiere que el país destinatario tenga nivel adecuado de protección
  - [VERIFICAR VIGENCIA: la lista de países reconocidos con nivel adecuado por Argentina — verificar resoluciones AAIP vigentes al momento de implementar]
  - EE.UU.: no tiene reconocimiento automático — verificar si el receptor está certificado bajo algún mecanismo bilateral vigente

- [ ] **Si no hay nivel adecuado: verificar mecanismo de legitimación aplicable**
  - Cláusulas contractuales tipo aprobadas por AAIP
  - Consentimiento explícito del titular para la transferencia (menos robusto como mecanismo general)
  - BCR (Binding Corporate Rules) para grupos empresariales multinacionales

- [ ] **Mencionar las transferencias en la Privacy Policy**
  - Indicar países destinatarios
  - Indicar el mecanismo de legitimación usado para cada transferencia

---

## Fase 5 — Si tenés o esperás usuarios en la Unión Europea

- [ ] **Verificar si aplica el GDPR**
  - Art. 3 GDPR: aplica si ofrecés bienes o servicios a personas en la UE o si monitoreás su comportamiento, aunque no tengas establecimiento físico en Europa
  - Signo de que aplica: tu sitio está en inglés o en idiomas de la UE, aceptás pagos en EUR, tu marketing menciona países de la UE

- [ ] **Si aplica GDPR: nombrar representante en la UE**
  - Art. 27 GDPR: obligatorio para organizaciones fuera de la UE que ofrecen servicios a residentes de la UE
  - El representante es una persona física o jurídica en la UE que actúa en nombre de la empresa ante las autoridades supervisoras
  - Existen servicios especializados de representación GDPR para startups

- [ ] **Preparar Privacy Policy dual (Ley 25.326 + adenda GDPR)**
  - Una sección para usuarios argentinos bajo Ley 25.326
  - Una adenda o sección separada para usuarios de la UE bajo GDPR, con base legal para cada tratamiento, derechos adicionales (portabilidad, oposición), datos del representante en UE

- [ ] **Implementar consent management platform (CMP) para cookies**
  - Bajo GDPR: las cookies no esenciales requieren consentimiento previo e informado (opt-in)
  - Herramientas: Cookiebot, OneTrust, Axeptio, o implementación propia con registro de consentimiento
  - El banner de cookies genérico "al continuar navegando aceptás" NO es válido bajo GDPR

---

## Fase 6 — Contratos con clientes (B2B o B2C)

- [ ] **MSA / TyC revisados por abogado antes de usar con clientes reales**
  - Un modelo genérico de internet sin adaptación argentina tiene riesgos reales: jurisdicción inválida, cláusulas abusivas bajo LDC, vacíos en la regulación de datos
  - Ver `contratos/modelos/` para los modelos base de este repositorio

- [ ] **Cláusula de liability cap definida (para B2B)**
  - Típico en SaaS: limitar la responsabilidad total al importe de las cuotas pagadas en los últimos 12 meses
  - Sin cláusula de liability cap: en caso de incidente podés enfrentar reclamos sin límite

- [ ] **SLA con uptime comprometido y tabla de créditos con CAP**
  - Definir: porcentaje de uptime comprometido (99.9% es estándar), ventana de medición (mes calendario), qué cuenta como downtime (excluir mantenimientos programados, fuerza mayor)
  - CAP de créditos: el total de créditos en un período no puede superar el valor de la cuota mensual

- [ ] **Jurisdicción definida explícitamente**
  - Para B2B: City of Buenos Aires o CABA, tribunales ordinarios en lo comercial
  - Para B2C: [VERIFICAR VIGENCIA: restricciones LDC sobre cláusulas de adhesión y foro]
  - Cláusula de ley aplicable: República Argentina, sin perjuicio de normas de orden público

---

## Nota final

Este checklist no reemplaza el asesoramiento legal profesional. Su función es que llegues a la reunión con tu abogado con los puntos críticos ya identificados, los contratos que necesitás firmados, y las decisiones de diseño de producto que afectan el cumplimiento ya tomadas. El tiempo que te cuesta completarlo ahora es una fracción del costo de resolver incumplimientos con usuarios reales.
