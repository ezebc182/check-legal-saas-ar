# Caso 02 — SaaS B2C Fintech: "CuentaYa"

> Caso ficticio. Empresa, nombre, DNI y datos inventados. El objetivo es mostrar
> exactamente qué output produce el perfil legal ante este tipo de producto.

---

## 1. Descripción del caso

| Campo                 | Detalle                                                                     |
| --------------------- | --------------------------------------------------------------------------- |
| **Empresa ficticia**  | CuentaYa S.A.S. (CUIT 30-71987654-3)                                        |
| **Producto**          | Aplicación móvil y web: billetera virtual, pagos QR, préstamos personales y tarjeta prepaga para consumidores argentinos |
| **Modelo de negocio** | B2C — consumidores finales mayores de 18 años; sin intermediarios empresariales |
| **Precio**            | Freemium: billetera gratuita, comisión por préstamos, spread en cambio de moneda |
| **Datos tratados**    | Ver sección 1.1                                                             |
| **Infraestructura**   | GCP us-central1 (Iowa, EE.UU.) con base de datos PostgreSQL en Cloud SQL     |
| **Regulación sectorial** | Proveedor de Servicios de Pago (PSP) bajo normativa BCRA [VERIFICAR VIGENCIA: Comunicaciones BCRA vigentes para PSP] |

### 1.1 Catálogo de datos tratados

**Datos de identificación y contacto (art. 2 Ley 25.326 — datos comunes):**
- Nombre completo, DNI, CUIL/CUIT
- Fecha de nacimiento, nacionalidad
- Domicilio, email, teléfono celular
- Selfie para validación de identidad (biometría facial) — potencialmente dato sensible

**Datos financieros:**
- Historial de transacciones dentro de la plataforma
- Saldo de billetera virtual
- Historial de préstamos y pagos
- Score crediticio interno calculado por CuentaYa
- Consultas a Veraz / Sistema de Información de Deudores del BCRA

**Datos de comportamiento:**
- Patrones de uso de la app (frecuencia, horarios, dispositivo)
- Geolocalización al momento de transacciones (opcional)

---

## 2. Variables de configuración para el perfil

```yaml
MODELO_NEGOCIO: "B2C"
TIPO_USUARIOS: "consumidores_finales"
APLICA_LDC: true  # Ley 24.240 — obligatorio en B2C con consumidores argentinos

DATOS_COMUNES:
  - nombre_dni_cuil_cuil
  - domicilio_email_telefono
  - fecha_nacimiento_nacionalidad

DATOS_POTENCIALMENTE_SENSIBLES:
  - biometria_facial: true  # selfie para validación KYC

DATOS_FINANCIEROS:
  - historial_transacciones
  - score_crediticio_interno
  - consultas_a_veraz_bcr

TRANSFERENCIAS_INTERNACIONALES: true
DESTINO_TRANSFERENCIA: "GCP us-central1 (EE.UU.)"
NIVEL_ADECUACION_DESTINO: null  # EE.UU. no tiene nivel adecuado reconocido por Argentina

JURISDICCION_USUARIOS: "Argentina"

TIPO_CONTRATO_CON_USUARIO: "contrato_de_adhesion"  # TyC que el usuario acepta sin negociar
TIENE_CLAUSULA_ARBITRAJE: null  # A verificar — ver red-flags
TIENE_BOTON_DE_BAJA: null       # A verificar — obligatorio bajo LDC
TIENE_RENOVACION_AUTOMATICA: null  # A verificar

REGULACION_SECTORIAL: "PSP_BCRA"  # Proveedor de Servicios de Pago
```

---

## 3. Análisis que produce el perfil

### 3.1 Estatuto del consumidor — LDC Ley 24.240 aplica sin excepción

**[MARCO OBLIGATORIO — LEY 24.240 DE DEFENSA DEL CONSUMIDOR]**

CuentaYa tiene como usuarios a consumidores finales argentinos. La Ley 24.240 (LDC) aplica de forma imperativa. El contrato entre CuentaYa y sus usuarios es un **contrato de adhesión** (el usuario solo puede aceptar o rechazar, no negociar las cláusulas).

Consecuencias directas:

1. **Control de cláusulas abusivas** (art. 37 LDC): Las cláusulas que desnaturalicen las obligaciones de CuentaYa, limiten la responsabilidad por daños o impongan condiciones injustas son nulas de pleno derecho. El juez puede declarar la nulidad aunque el usuario las haya "aceptado" haciendo clic.

2. **Interpretación a favor del consumidor** (art. 37 in fine LDC): En caso de duda sobre el alcance de una cláusula, se interpreta a favor del consumidor.

3. **Información adecuada** (art. 4 LDC): El usuario debe recibir información "cierta, clara y detallada" sobre los servicios, costos, riesgos y condiciones. Los TyC en letra chica o lenguaje técnico-legal no cumplen este requisito.

4. **CCCN art. 1119**: El CCCN (Código Civil y Comercial) complementa la LDC con controles adicionales sobre contratos de adhesión y cláusulas predispuestas. Si una cláusula sorprende al adherente o es abusiva, puede atacarse por esta vía además de la LDC.

---

### 3.2 Datos financieros — Consulta a Veraz/BCR

**[ANÁLISIS — DATOS DE SOLVENCIA PATRIMONIAL: art. 26 Ley 25.326]**

El art. 26 Ley 25.326 regula específicamente el tratamiento de datos de solvencia patrimonial (información crediticia):

> Art. 26: "En la prestación de servicios de información crediticia sólo pueden tratarse datos personales de carácter patrimonial relativos a la solvencia económica y al crédito, obtenidos de fuentes de acceso público irrestricto, o procedentes de informaciones facilitadas por el interesado o con su consentimiento."

[VERIFICAR VIGENCIA: el art. 26 Ley 25.326 — verificar si fue modificado y cuál es la interpretación actual de la AAIP sobre datos de solvencia en el contexto de fintech]

**Para CuentaYa:**

- Consultar el historial de un usuario en Veraz u otros bureaus requiere base legal. Lo más habitual en el sector: consentimiento expreso del usuario en el flujo de solicitud de préstamo.
- Ese consentimiento debe ser específico para la consulta de solvencia, no un consentimiento genérico enterrado en los TyC.
- El usuario tiene derecho a saber que se hizo la consulta y a los datos que Veraz tiene de él (habeas data).

---

### 3.3 Biometría facial — Potencial dato sensible

**[ALERTA — BIOMETRÍA FACIAL: POSIBLE DATO SENSIBLE]**

CuentaYa usa selfie + liveness detection para validar la identidad del usuario en el onboarding (KYC). Los datos biométricos que permiten identificación única de una persona son considerados datos sensibles en múltiples marcos regulatorios.

Bajo Ley 25.326, la categoría de "datos sensibles" incluye datos de salud, vida sexual, religión, opinión política y origen racial. La biometría no está expresamente mencionada en la ley original.

[VERIFICAR VIGENCIA: Si la AAIP ha emitido criterios o resoluciones que clasifiquen datos biométricos como sensibles bajo Ley 25.326. El proyecto de reforma de la ley de protección de datos personales en Argentina incluye biometría expresamente.]

**Riesgo actual:** En ausencia de categorización explícita, CuentaYa debería aplicar precautoriamente el régimen de datos sensibles a la información biométrica. Esto implica:
- Consentimiento expreso e informado para el tratamiento biométrico
- No usar la biometría para finalidades distintas al KYC (no para publicidad, no para scoring conductual)
- Medidas de seguridad Nivel ALTO
- Informar al usuario exactamente qué pasa con su selfie y si se comparte con terceros (ej: proveedor de liveness detection)

---

### 3.4 TyC B2C — Red-flags de la LDC

**[REVISIÓN TyC — PUNTOS CRÍTICOS BAJO LDC]**

#### Árbitro obligatorio

Las cláusulas que someten obligatoriamente al consumidor a arbitraje privado (en lugar de justicia ordinaria) están expresamente prohibidas por el art. 37 inc. b LDC:

> Art. 37 inc. b: "Se tendrán por no convenidas las cláusulas que (...) impongan la inversión de la carga de la prueba en perjuicio del consumidor."

Y la jurisprudencia de Cámaras comerciales ha extendido esto a cláusulas de arbitraje obligatorio que impidan al consumidor acudir a la justicia. Ver también: CCCN art. 1651 (contratos de adhesión y arbitraje).

[VERIFICAR VIGENCIA: Jurisprudencia CSJN y Cámaras sobre arbitraje en contratos de consumo]

#### Renovación automática sin aviso previo

Si los TyC incluyen renovación automática de suscripción o préstamo sin notificación previa, hay riesgo alto bajo LDC. El consumidor debe ser informado antes de la renovación.

La Resolución Secretaría de Comercio Interior sobre contratos de suscripción [VERIFICAR VIGENCIA: número de resolución] establece requisitos de notificación previa para renovaciones automáticas en contratos B2C digitales.

#### Botón de baja accesible

Resolución 1085/2023 de Secretaría de Comercio (o la que esté vigente) [VERIFICAR VIGENCIA] estableció que las plataformas digitales deben ofrecer un mecanismo de baja tan simple como el mecanismo de alta. Si el usuario se pudo dar de alta en 3 pasos, debe poder darse de baja en 3 pasos o menos.

Esto aplica directamente a CuentaYa: si el onboarding es digital, la baja debe ser digital, accesible y sin fricciones.

---

### 3.5 Privacy Policy — Requisitos bajo Ley 25.326

**[OBLIGACIÓN — POLÍTICA DE PRIVACIDAD]**

La política de privacidad de CuentaYa debe cumplir con el art. 6 Ley 25.326 (principio de información). Elementos mínimos:

- Quién trata los datos (CuentaYa S.A.S. con CUIT y domicilio)
- Qué datos se tratan y con qué finalidades
- Si los datos se comparten con terceros y quiénes son (ej: Veraz, proveedor de liveness, GCP)
- Que los datos se transfieren a EE.UU. y el mecanismo de legitimación
- Los derechos del titular: acceso, rectificación, supresión, confidencialidad (habeas data — art. 14 Ley 25.326)
- El canal para ejercer esos derechos (email, formulario) y el plazo de respuesta (art. 14: 5 días hábiles para dar acceso; 5 días para rectificar/suprimir)
- Si el score crediticio interno se usa para tomar decisiones automatizadas (ej: negar un préstamo), el usuario tiene derecho a conocer la lógica y a impugnar la decisión

---

### 3.6 Transferencia a GCP us-central1 — Sin nivel adecuado

**[ALERTA — TRANSFERENCIA INTERNACIONAL: GCP us-central1 (EE.UU.)]**

Misma problemática que otros SaaS que usan infraestructura estadounidense: EE.UU. no tiene nivel adecuado reconocido por Argentina.

Alternativa evaluada frecuentemente: GCP tiene región en Brasil (southamerica-east1, São Paulo). Sin embargo, Brasil no tiene decisión de adecuación de Argentina, así que migrar a GCP Brasil resuelve el problema de jurisdicción de la nube pero no elimina la necesidad de un mecanismo de legitimación para la transferencia.

[VERIFICAR VIGENCIA: Si GCP ha habilitado algún mecanismo de cláusulas contractuales específicamente validado por la AAIP argentina]

---

## 4. Red-flags específicas del caso con propuesta de corrección

### RF-01: Cláusula de arbitraje obligatorio

```
RIESGO: Los TyC incluyen cláusula que somete al usuario a arbitraje
        privado como única vía de resolución de conflictos.

IMPACTO: [RED FLAG — NULIDAD ABSOLUTA]
         Art. 37 inc. b LDC — nula de pleno derecho.
         No requiere que el usuario la impugne: el juez puede
         declararla nula de oficio.
         Además, incluir esta cláusula puede ser considerado
         práctica abusiva sancionable por la Secretaría de Comercio.

CORRECCIÓN PROPUESTA:
  Reemplazar con: "Ante cualquier conflicto, el usuario puede
  acudir a la justicia ordinaria con competencia en su domicilio,
  o alternativamente a mediación prejudicial voluntaria.
  CuentaYa acepta la competencia de los tribunales del domicilio
  del usuario."
  
  Opcionalmente: ofrecer arbitraje como mecanismo VOLUNTARIO
  y OPTATIVO, no obligatorio.
```

### RF-02: Renovación automática sin aviso

```
RIESGO: Los préstamos o suscripciones se renuevan automáticamente
        sin notificación previa al usuario.

IMPACTO: [RED FLAG — RIESGO ALTO: LDC art. 10 bis + normativa BCRA]
         El consumidor puede solicitar la reversión del cargo y
         CuentaYa debe reintegrar el dinero (arts. 10 bis y 52 bis LDC).
         Multa potencial de la Secretaría de Comercio.

CORRECCIÓN PROPUESTA:
  - Enviar email y push notification con al menos 15 días de
    anticipación antes de la renovación
  - Incluir enlace directo para cancelar desde la notificación
  - Registrar que la notificación fue enviada y recibida
```

### RF-03: Botón de baja no accesible o inexistente

```
RIESGO: El proceso de baja requiere contactar a soporte por email
        o Whatsapp y esperar respuesta.

IMPACTO: [RED FLAG — RIESGO ALTO: Resolución Secretaría de Comercio]
         Fricción artificial en la baja es práctica abusiva
         bajo el estatuto del consumidor.

CORRECCIÓN PROPUESTA:
  - Agregar opción "Cerrar cuenta" en el menú de perfil de la app
  - El flujo completo de baja no debe requerir interacción humana
    de CuentaYa (puede tener confirmación por email al usuario)
  - Aclarar qué pasa con el saldo al momento de la baja y
    con el historial de datos (derecho a la supresión)
```

### RF-04: Compartir datos con terceros sin disclosure explícito

```
RIESGO: Los TyC mencionan genéricamente "podremos compartir sus
        datos con terceros de confianza" sin identificarlos.

IMPACTO: [RED FLAG — RIESGO MEDIO: art. 6 Ley 25.326]
         El principio de información requiere identificar los
         destinatarios o categorías de destinatarios.

CORRECCIÓN PROPUESTA:
  Listar en la política de privacidad:
  - Proveedor de liveness/KYC: [nombre del proveedor]
  - Bureaus crediticios: Veraz / BCRA (con base legal específica)
  - Proveedor de infraestructura: Google Cloud (GCP us-central1, EE.UU.)
  - Procesador de pagos: [nombre si aplica]
  - Herramientas de analytics: [listar si se usan GA, Mixpanel, etc.]
```

---

## 5. Consulta de ejemplo al modelo con el perfil cargado

### Pregunta del usuario (founder o abogado de CuentaYa):

> "¿Puedo incluir una cláusula en los TyC que diga que el usuario acepta arbitraje obligatorio en caso de conflicto con CuentaYa?"

### Respuesta esperada del modelo con el perfil check-legal-saas-ar cargado:

```
[RED FLAG — NULIDAD ABSOLUTA: art. 37 inc. b LDC]

No. En contratos B2C argentinos, la cláusula de arbitraje OBLIGATORIO
es nula de pleno derecho bajo el art. 37 inc. b de la Ley 24.240.
El problema no es solo que el juez podría invalidarla: es que incluirla
puede ser en sí misma una práctica abusiva sancionable por la
Secretaría de Comercio con multa (art. 47 LDC).

Por qué no funciona el argumento "el usuario la aceptó":
El art. 37 LDC establece que se tienen por "no convenidas" ciertas
cláusulas independientemente del consentimiento del usuario. El
consentimiento no purga la nulidad de una cláusula abusiva.

Qué sí podés hacer:
1. MEDIACIÓN PREJUDICIAL VOLUNTARIA: Ofrecer mediación como paso
   previo voluntario para resolver conflictos. No obligatorio, y
   el usuario siempre puede ir a la justicia directamente.

2. ARBITRAJE OPTATIVO: Incluir una cláusula que diga que el usuario
   "puede optar" por someter el conflicto a arbitraje, pero que no
   esté obligado a hacerlo y que siempre conserve el derecho de
   acudir a la justicia ordinaria.

3. COMPETENCIA TERRITORIAL FAVORABLE AL USUARIO: Aceptar la
   competencia de los tribunales del domicilio del usuario
   (art. 36 y 37 LDC), no imponer fuero propio de CuentaYa.

Redacción alternativa sugerida:
"Ante cualquier controversia, las partes podrán intentar una
solución amigable. Sin perjuicio de ello, el usuario podrá
acudir en cualquier momento a la justicia ordinaria con
competencia en su domicilio, o a los organismos de defensa
del consumidor. El arbitraje es una opción voluntaria que
deberá acordarse por escrito al momento del conflicto."

Esta redacción es legalmente válida bajo LDC + CCCN y no
expone a CuentaYa a sanciones por cláusulas abusivas.
```

---

*Licencia: Apache 2.0 — ver LICENSE en la raíz del repositorio.*
*Este caso es completamente ficticio. No constituye asesoramiento legal.*
*[VERIFICAR VIGENCIA: art. 26 Ley 25.326 sobre datos de solvencia patrimonial]*
*[VERIFICAR VIGENCIA: Resolución Secretaría de Comercio sobre baja digital y renovación automática]*
*[VERIFICAR VIGENCIA: Clasificación de biometría facial bajo Ley 25.326 argentina]*
