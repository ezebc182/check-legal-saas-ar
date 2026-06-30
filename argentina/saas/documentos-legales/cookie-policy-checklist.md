# Checklist: Cookie Policy para SaaS argentino
## Marco normativo: Ley 25.326 + Disposición AAIP 47/2018 + régimen UE (si aplica)

---

> **ADVERTENCIA NORMATIVA**
>
> La Ley 25.326 **no regula cookies expresamente**. La Disposición AAIP 47/2018 introdujo
> lineamientos sobre tecnologías de seguimiento y tratamiento de datos en entornos digitales
> [VERIFICAR VIGENCIA: Disposición AAIP 47/2018 — verificar si fue reemplazada o complementada
> por resoluciones posteriores].
>
> La guía de buenas prácticas de la AAIP sobre tracking digital también es referencia, aunque
> no tiene fuerza normativa vinculante con el mismo rango que la ley [VERIFICAR VIGENCIA].
>
> Si el SaaS tiene usuarios en la UE: el GDPR + la Directiva ePrivacy (2002/58/CE, con proyecto
> de reemplazo por el ePrivacy Regulation aún en negociación al 2026) exigen consentimiento
> previo e informado para cookies no esenciales. Ese régimen es independiente del argentino y
> más exigente.

---

## Clasificación de cookies: checklist de identificación

Antes de redactar la Cookie Policy, identificá qué tipos de cookies usa el SaaS. Completá este inventario:

### 1. Cookies esenciales / técnicas

- [ ] Cookies de sesión (mantienen al usuario logueado)
- [ ] Cookies de seguridad (CSRF token, protección de formularios)
- [ ] Cookies de preferencias básicas del usuario (idioma, región)
- [ ] Cookies de carrito o proceso de pago en curso

**Tratamiento bajo ley argentina**: Su uso es legítimo sin consentimiento expreso porque son necesarias para prestar el servicio. Deben estar listadas e informadas, pero no requieren opt-in.

**Tratamiento bajo régimen UE**: Igual — exentas del requisito de consent.

---

### 2. Cookies funcionales

- [ ] Cookies que recuerdan el layout preferido del usuario
- [ ] Cookies que guardan configuraciones no esenciales (tamaño de fuente, modo oscuro, idioma elegido más allá del idioma del navegador)
- [ ] Cookies de chat en vivo (ej: Intercom, Crisp, HubSpot Chat)

**Tratamiento bajo ley argentina**: Requieren información clara. Consentimiento recomendado aunque no exigido expresamente por la ley vigente.

**Tratamiento bajo régimen UE**: Requieren consentimiento previo si no son estrictamente necesarias para el servicio contratado.

---

### 3. Cookies analíticas

- [ ] Google Analytics (GA4) — identificar si está configurado con IP anonymization y sin User ID cross-site
- [ ] Mixpanel
- [ ] Amplitude
- [ ] Hotjar / Microsoft Clarity (grabaciones de sesión + heatmaps)
- [ ] Segment
- [ ] PostHog (self-hosted vs cloud — diferencia en tratamiento)

**Tratamiento bajo ley argentina**: Requieren información al usuario y mecanismo de opt-out. La Disposición AAIP 47/2018 señala la necesidad de informar sobre tecnologías de seguimiento [VERIFICAR VIGENCIA: Disposición AAIP 47/2018].

**Tratamiento bajo régimen UE**: Consentimiento previo obligatorio para cualquier herramienta de analytics que genere identificadores persistentes o perfiles de comportamiento.

---

### 4. Cookies de marketing / retargeting

- [ ] Meta Pixel (Facebook/Instagram Ads)
- [ ] Google Ads / Google Tag Manager con etiquetas de conversión
- [ ] LinkedIn Insight Tag
- [ ] TikTok Pixel
- [ ] Snap Pixel
- [ ] Twitter/X Ads Pixel
- [ ] Microsoft Ads (Bing)

**Tratamiento bajo ley argentina**: Consentimiento previo recomendado; la ausencia de información sobre estas cookies es un incumplimiento del deber de informar (art. 6 Ley 25.326 aplicado al contexto digital). [RED FLAG: muchos SaaS argentinos instalan Meta Pixel sin mencionar en ningún documento que existe]

**Tratamiento bajo régimen UE**: Consentimiento previo **obligatorio** bajo GDPR + ePrivacy. Sin banner de consent y opt-in real: violación directa.

---

## Contenido mínimo recomendado para la Cookie Policy

### A. Explicación general

- [ ] Qué es una cookie (definición accesible, sin jerga técnica excesiva)
- [ ] Por qué el SaaS usa cookies (finalidades por categoría)
- [ ] Duración de las cookies (sesión vs persistentes — indicar duración en días/meses para cada una en la tabla)

### B. Tabla de cookies por categoría

La tabla debe contener al menos:

| Columna | Descripción |
|---|---|
| Nombre de la cookie | Nombre técnico exacto (ej: `_ga`, `_fbp`, `JSESSIONID`) |
| Categoría | Esencial / Funcional / Analítica / Marketing |
| Proveedor | Propio / Google / Meta / etc. |
| Finalidad | Descripción específica (no genérica) |
| Duración | Sesión / X días / X meses / permanente |
| Datos que recopila | IP, comportamiento de navegación, identificador de dispositivo, etc. |

- [ ] Tabla completa de cookies propias
- [ ] Tabla completa de cookies de terceros (con el nombre del proveedor y link a su política de privacidad)
- [ ] Si usás Google Tag Manager: aclarar que GTM puede cargar etiquetas adicionales y que la lista de cookies se actualiza cuando se publican nuevas etiquetas

### C. Cookies de terceros identificadas nominalmente

- [ ] Cada proveedor de cookies de terceros identificado por nombre
- [ ] Link a la política de privacidad de cada proveedor
- [ ] Aclaración de que esos terceros tienen sus propias políticas sobre las que el SaaS no tiene control

### D. Cómo deshabilitar cookies por navegador

- [ ] Instrucción de cómo deshabilitar cookies en Chrome (link a `chrome://settings/cookies`)
- [ ] Instrucción para Firefox (link a `about:preferences#privacy`)
- [ ] Instrucción para Safari (Preferencias → Privacidad)
- [ ] Instrucción para Edge (link a `edge://settings/content/cookies`)
- [ ] Advertencia: deshabilitar cookies esenciales puede impedir el uso del servicio

### E. Opt-out de rastreo cross-site

- [ ] Si hay cookies de marketing o analíticas con seguimiento cross-site: mecanismo de opt-out documentado
- [ ] Para Google Analytics: link a `https://tools.google.com/dlpage/gaoptout` y/o instrucciones de configuración de GA4 con consent mode
- [ ] Para Meta Pixel: link al Centro de preferencias de Meta (`https://www.facebook.com/privacy/consent/`)
- [ ] Opt-out de publicidad basada en intereses: link a `https://optout.aboutads.info` (DAA) y/o `https://www.youronlinechoices.com` (EDAA para UE)

### F. Para usuarios en la UE: Consent Management Platform (CMP)

- [ ] Banner de consentimiento previo que se muestra **antes** de instalar cookies no esenciales (no después)
- [ ] El banner permite aceptar, rechazar o configurar por categoría — no solo "Aceptar todo"
- [ ] El rechazo es tan fácil como la aceptación (botón visible de igual jerarquía visual)
- [ ] El consentimiento se registra con timestamp y versión del documento
- [ ] El usuario puede cambiar sus preferencias en cualquier momento (link en el footer)
- [ ] CMP integrado con los sistemas de analytics y ads para que no se disparen sin consent

Herramientas CMP compatibles con GDPR: Cookiebot, OneTrust, Usercentrics, Axeptio, Iubenda. [VERIFICAR VIGENCIA: verificar compatibilidad con la versión actual del GDPR y ePrivacy Regulation si ya fue adoptado]

---

## Red-flags: errores frecuentes en Cookie Policy de SaaS argentino

- [ ] **Meta Pixel o Google Ads instalados sin mención en la Cookie Policy**: si el pixel está en el código y no aparece en el documento, el documento es incompleto [RED FLAG]
- [ ] **Cookie Policy con tabla vacía o con "próximamente"**: un documento que promete información sin proveerla no cumple con el deber de informar [RED FLAG]
- [ ] **Cookies de marketing activadas antes del consent del usuario en UE**: el pixel se dispara en el `pageload` sin esperar consent = violación GDPR directa [RED FLAG crítico para usuarios en UE]
- [ ] **Google Analytics sin configurar consent mode en GA4**: desde 2024 Google requiere Consent Mode v2 para los mercados europeos; sin él, los datos de conversión pueden perderse y el cumplimiento GDPR es cuestionable [VERIFICAR VIGENCIA: requisitos de Google Consent Mode v2]
- [ ] **Hotjar / Microsoft Clarity sin mención de grabación de sesión**: estas herramientas capturan comportamiento del usuario en detalle; no mencionarlo es una omisión significativa
- [ ] **Duración de cookies no especificada**: decir "cookies de sesión y persistentes" sin indicar cuánto duran es información incompleta
- [ ] **Links a políticas de terceros rotos o desactualizados**: verificar que los links a Google, Meta, LinkedIn, etc. siguen activos
- [ ] **Cookie Policy sin fecha de última actualización**: imposible saber si está vigente [RED FLAG]
- [ ] **GTM instalado pero no listado**: Google Tag Manager en sí no es una cookie, pero es el contenedor que carga otras; mencionarlo y aclarar qué etiquetas activas tiene es buena práctica
