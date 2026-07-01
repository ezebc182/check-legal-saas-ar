# check-legal-saas-ar

Plugin de Claude Code para revisar el estado legal de tu SaaS argentina: TyC, Privacy Policy, contratos y protección de datos bajo Ley 25.326.

---

## ¿Para qué sirve?

Pegás tus TyC y en 30 segundos sabés si tenés cláusulas nulas, qué le falta a tu Privacy Policy, o si el contrato con tu cliente empresarial te expone.

Por ejemplo, le mandás esto:

> *"Acá están nuestros TyC. Somos B2C, cobramos suscripción mensual."*

Y obtenés:

```
[RED FLAG - NULIDAD ABSOLUTA] Cláusula 8.3: arbitraje obligatorio.
Nula de pleno derecho bajo art. 37 inc. b LDC. El usuario puede ignorarla
y recurrir a la justicia ordinaria de todos modos.

[RED FLAG - RIESGO ALTO] No hay mecanismo de cancelación accesible.
Bajo LDC la cancelación no puede ser más difícil que la contratación.

[RED FLAG - RIESGO ALTO] Precio en dólares sin tipo de cambio de referencia.
Riesgo de reclamo de consumidor por indeterminación del precio.

Cláusulas obligatorias ausentes: identificación del proveedor con CUIT,
domicilio legal en Argentina, procedimiento de notificación de cambios en TyC.
```

No es un análisis genérico. Aplica Ley 25.326, LDC, CCCN — no el GDPR europeo.

---

## Instalación (Claude Code)

```bash
/plugin marketplace add https://github.com/ezebc182/check-legal-saas-ar
/plugin install check-legal-saas-ar
```

Reiniciá Claude Code. Listo.

---

## Comandos disponibles

| Comando | Qué hace |
|---|---|
| `/check-legal-saas-ar:diagnostico` | 5 preguntas rápidas → diagnóstico de riesgo general de tu SaaS |
| `/check-legal-saas-ar:revisar-tyc` | Analizá tus Términos y Condiciones (B2B o B2C) |
| `/check-legal-saas-ar:revisar-privacypolicy` | Auditá tu Privacy Policy bajo Ley 25.326 |
| `/check-legal-saas-ar:revisar-contratos` | Revisá MSA, DPA o NDA de desarrollo |

**Empezá por el diagnóstico:**

```
/check-legal-saas-ar:diagnostico MiSaaS
```

Te hace 5 preguntas (modelo de negocio, datos que tratás, si tenés AAIP, etc.) y te dice qué revisar primero.

---

## Qué cubre

- **TyC y contratos B2C** — cláusulas abusivas, estatuto del consumidor (LDC Ley 24.240), derechos irrenunciables, renovación automática, botón de baja
- **TyC y contratos B2B** — SLA, liability cap, AUP, propiedad intelectual de customizaciones, DPA obligatorio
- **Privacy Policy** — contenido mínimo bajo art. 6 Ley 25.326, vocabulario correcto (no GDPR), datos sensibles bajo art. 7
- **DPA** — cuándo es obligatorio, qué tiene que decir, red-flags de cláusulas que te exponen
- **NDA con freelancers** — si no hay cesión de IP explícita, el contratista se queda con el código (Ley 11.723)
- **Inscripción AAIP** — si no inscribiste tu base de datos, ya estás en infracción (art. 21 Ley 25.326)
- **Transferencias internacionales** — AWS, GCP, Stripe: qué implica bajo art. 12 Ley 25.326
- **Expansión LATAM/UE** — qué cambia al tener usuarios en Chile, Colombia, Brasil o la UE

---

## Sin Claude Code

**Claude.ai (plan Pro o Team):**
1. Descargá `argentina/saas/saas-CLAUDE.md`
2. En tu Project → **Knowledge** → subí el archivo
3. Todos los chats del Project tienen el perfil activo

**Cualquier otro modelo (GPT, Gemini, etc.):**
Copiá el contenido de `argentina/saas/saas-CLAUDE.md` y pegalo como system prompt al inicio de la conversación.

---

## Qué NO hace

- No reemplaza al abogado. Identifica problemas; el abogado los resuelve.
- No da opinión legal sobre tu caso específico.
- No garantiza análisis exhaustivo.

---

## Contribuir

Apache 2.0. Errores normativos → issue. Nueva área del derecho (laboral, tributario, societario) → PR siguiendo `CONTRIBUTING.md`.

---

*Basado en [claude-for-legal](https://github.com/anthropics/claude-for-legal) de Anthropic (Apache 2.0) · Mantenido por [ezebc182](https://github.com/ezebc182)*
