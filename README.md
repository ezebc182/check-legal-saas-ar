# check-legal-saas-ar

Perfiles de práctica legal para empresas SaaS operando en Argentina, diseñados para usarse con asistentes de IA (Claude, GPT, Gemini, etc.) como contexto de sistema.

## ¿Qué es esto?

Un conjunto de archivos Markdown que convertís en el "cerebro legal" de tu asistente de IA. Cargás el perfil que corresponde a tu consulta, y el modelo responde con criterio legal argentino: cita las normas correctas, levanta red flags reales, usa el vocabulario de la Ley 25.326 (no del GDPR europeo), y te dice qué verificar antes de asumir que algo está vigente.

No reemplaza al abogado. Te ayuda a llegar a la reunión con el abogado sabiendo qué preguntar.

## Cobertura actual

| Área | Archivo | Estado |
|---|---|---|
| SaaS · compliance integral | `argentina/saas/saas-CLAUDE.md` | ✅ Disponible |
| Protección de datos · Ley 25.326 | `argentina/proteccion-datos-CLAUDE.md` | 🔜 Próximamente |
| Contratos B2B y B2C | `argentina/contratos/CLAUDE.md` | 🔜 Próximamente |
| Propiedad intelectual del software | `argentina/ip-software-CLAUDE.md` | 🔜 Próximamente |

## Instalación rápida

### Claude Code / Claude Desktop (recomendado)

1. Cloná el repo:
   ```bash
   git clone https://github.com/ezebc182/check-legal-saas-ar.git
   ```

2. En tu proyecto, creá o editá `CLAUDE.md` y agregá:
   ```
   Lee el archivo argentina/saas/saas-CLAUDE.md como perfil de práctica legal.
   ```

3. Alternativamente, en Claude Code:
   ```
   /plugin marketplace add /ruta/a/check-legal-saas-ar
   ```

### Claude.ai Projects (Plan Pro/Team)

1. Descargá los archivos `.md` que necesitás.
2. En tu Project de Claude, andá a **Knowledge** → subí los archivos.
3. Todos los chats del Project tendrán el perfil activo.

### Cualquier otro modelo

Copiá el contenido del perfil que necesitás y pegalo como contexto de sistema (system prompt) o al inicio de la conversación.

## Cómo usar el perfil SaaS

Una vez cargado `argentina/saas/saas-CLAUDE.md`, el modelo puede:

- **Revisar Términos y Condiciones** → pedile que analice el documento; el perfil corre el flujo de red-flags automáticamente
- **Revisar Privacy Policy** → identifica qué falta bajo Ley 25.326 y qué vocabulario está mal
- **Checklist de compliance** → preguntale "¿qué obligaciones de protección de datos tenemos?"
- **Protección de IP** → "¿quién es dueño del código que desarrolló nuestro contratista freelance?"
- **Contratos B2B/B2C** → "analizá este SLA y decime los riesgos para nosotros como proveedor"

**Configuración inicial:** al inicio de la sesión, informale al modelo estas variables:

```
MODELO_NEGOCIO: B2B / B2C / B2B2C
DATOS_TRATADOS: comunes / sensibles (salud, etc.)
TRANSFERENCIAS_INTERNACIONALES: sí (AWS us-east-1) / no
JURISDICCION_CLIENTES: Argentina / Argentina + UE / etc.
```

## Convenciones del repo

- `[VERIFICAR VIGENCIA: ...]` — alerta de que esa norma puede haber cambiado; verificar antes de asesorar
- `[RED FLAG - NULIDAD ABSOLUTA]` — cláusula inválida de pleno derecho bajo derecho argentino
- `[RED FLAG - RIESGO ALTO]` — cláusula que genera riesgo legal significativo; requiere atención inmediata
- `[RED FLAG - RIESGO MEDIO]` — cláusula subóptima; corregir en próxima revisión
- `[VACÍO PROBATORIO]` — falta jurisprudencia o doctrina específica; indicar al cliente

## Contribuir

Este repo es open source (Apache 2.0). Las contribuciones son bienvenidas:

- **Nuevas áreas del derecho:** laboral, tributario, societario, consumidor
- **Modelos de contratos:** MSA, DPA, NDA con cláusula de IP para freelancers
- **Checklists:** inscripción AAIP, auditoría de seguridad, breach notification
- **Correcciones normativas:** si una norma cambió, abrí un PR con la actualización

### Cómo contribuir

1. Fork del repo
2. Creá una rama: `git checkout -b feat/laboral-CLAUDE`
3. Seguí las convenciones de marcadores arriba
4. Abrí un PR con descripción de qué área cubre y qué normas referencia

**Importante:** los perfiles deben referenciar normativa argentina vigente, incluir marcadores `[VERIFICAR VIGENCIA]` donde la norma es de vigencia variable, y NO usar terminología GDPR cuando el contexto es exclusivamente argentina (Ley 25.326).

## Advertencia legal

Este repositorio es material de referencia y formación. No constituye asesoramiento jurídico. Cada consulta real requiere un abogado matriculado que conozca las particularidades del caso.

## Licencia

Apache License 2.0 — ver [LICENSE](LICENSE).

Basado en el proyecto [claude-for-legal](https://github.com/anthropics/claude-for-legal) de Anthropic, Inc., publicado bajo Apache 2.0.

---

*Mantenido por [ezebc182](https://github.com/ezebc182)*
