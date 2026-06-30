# Roadmap — check-legal-saas-ar

Este documento describe la dirección del proyecto. Las fechas son orientativas; el avance real depende de contribuciones de la comunidad y disponibilidad de los mantenedores.

---

## Estado actual

```
v1.0.0 — Junio 2026
Perfil SaaS integral para Argentina
```

---

## Fase 1 — Perfil SaaS integral (ACTUAL ✓)

**Objetivo**: un único perfil de práctica que cubra las áreas del derecho más frecuentes para una SaaS argentina, desde la etapa de constitución hasta la escala internacional.

### Entregables completados

- [x] `argentina/saas-CLAUDE.md` — Perfil principal
- [x] Cobertura Ley 25.326 (Protección de Datos Personales)
- [x] Cobertura Ley 11.723 (Propiedad Intelectual / Software)
- [x] Cobertura Ley 24.766 (Confidencialidad)
- [x] Cobertura Ley 22.362 (Marcas)
- [x] Cobertura Ley 24.240 (Defensa del Consumidor)
- [x] Cobertura CCCN — contratos, responsabilidad, jurisdicción
- [x] README, LICENSE (Apache 2.0), QUICKSTART, CHANGELOG, SECURITY, CODE_OF_CONDUCT

### En revisión continua

- Actualizaciones normativas de la AAIP (disposiciones y resoluciones)
- Evolución jurisprudencial de cámaras y CSJN en materia de datos, IP y consumo digital
- Nuevas guías y recomendaciones de organismos internacionales con impacto local (Grupo de Berlín, OCDE, GDPR — en la medida en que Argentina busca adecuación)

---

## Fase 2 — Plantillas y checklists accionables (próximos 3-6 meses)

**Objetivo**: pasar de _comprensión_ a _ejecución_. Que un operador SaaS pueda no solo entender qué necesita, sino tener un punto de partida concreto para sus documentos legales.

### Modelos de contratos

- [ ] **MSA B2B (Master Service Agreement)**: acuerdo marco de servicios entre empresas, con cláusulas adaptadas al servicio SaaS (SLA, uptime, responsabilidad limitada, auditoría, terminación).
- [ ] **Términos y Condiciones B2C**: para plataformas con usuarios finales personas humanas; incluye consideraciones LDC, derecho de arrepentimiento, limitación de responsabilidad.
- [ ] **DPA (Data Processing Agreement)**: acuerdo de tratamiento de datos para contratos con proveedores cloud y subencargados; compatible con Ley 25.326 y con cláusulas de adecuación para DPA GDPR.
- [ ] **NDA con cláusula IP**: acuerdo de confidencialidad para contratación de freelancers, desarrolladores y agencias; incluye asignación de derechos de propiedad intelectual conforme Ley 11.723.
- [ ] **Contrato de locación de obra (software a medida)**: modelo para contratación de desarrollo externo con cláusulas de entrega, propiedad del código, garantías y mantenimiento.

### Checklists de cumplimiento

- [ ] **Checklist: Política de Privacidad (Ley 25.326)** — qué información debe contener obligatoriamente, qué es opcional pero recomendable, qué es incorrecto incluir.
- [ ] **Checklist: Cookie Policy** — categorías de cookies, consentimiento, banner legal, relación con Ley 25.326 y estándares internacionales.
- [ ] **Checklist: Inscripción RNBD (AAIP)** — paso a paso del trámite en la plataforma de la AAIP, campos requeridos, plazos, renovación.
- [ ] **Checklist: Lanzamiento legal de SaaS B2C** — todo lo que necesitás tener antes de publicar una app al público en Argentina.
- [ ] **Checklist: Due Diligence legal para fundraising** — qué documentación legal exigen los inversores y en qué estado deberías tenerla.

---

## Fase 3 — Expansión de áreas y jurisdicciones (futuro)

**Objetivo**: ampliar el alcance del proyecto a otras áreas del derecho relevantes para equipos tech y a otros países de la región.

### Nuevas áreas del derecho argentino

- [ ] **Perfil laboral para equipos tech**: contratación de empleados en relación de dependencia (LCT), trabajo remoto, pasantías, monotributistas vs. empleados, Convenio Colectivo de Trabajo de Sistemas (SECLO), beneficios no remunerativos.
- [ ] **Perfil tributario para SaaS**: facturación de servicios digitales B2B y B2C, IVA en servicios digitales exportados, facturación a clientes del exterior, relación AFIP — monotributo vs. responsable inscripto para SaaS, retenciones.
- [ ] **Perfil IP del software avanzado**: patentes de software en Argentina (estado actual, viabilidad, alternativas), Open Source (licencias GPL/MIT/Apache y sus implicancias comerciales), contribución a proyectos open source como empleado.
- [ ] **Perfil societario y fundraising**: tipos societarios para startups (SAS, SA, SRL), pactos de accionistas, cap table, inversión ángel, seed, Series A bajo ley argentina y estructuras Delaware/Cayman para inversores extranjeros.

### Expansión a otras jurisdicciones LATAM

La expansión regional se hará con el mismo modelo: perfiles basados en la normativa local, mantenidos por colaboradores con conocimiento del derecho de cada país.

- [ ] **Uruguay** — Ley 18.331 (Protección de Datos), régimen de software, zonas francas digitales.
- [ ] **Chile** — Ley 19.628 (en transición hacia nueva ley), Ley 20.169 (competencia desleal en digital), régimen de propiedad intelectual.
- [ ] **Colombia** — Ley 1581 de 2012 (Habeas Data), Ley 23 de 1982 (derechos de autor), SIC como autoridad de datos.
- [ ] **México** — LFPDPPP, IMPI para marcas y software, contratos de desarrollo bajo legislación federal.
- [ ] **Brasil** — LGPD (Lei Geral de Proteção de Dados), Marco Civil da Internet, registro de software en INPI.

---

## Cómo contribuir a esta hoja de ruta

Si querés trabajar en alguno de estos ítems:

1. Abrí un issue mencionando el ítem de la Fase 2 o 3 que querés abordar.
2. El equipo lo triagea y si hay acuerdo te asignamos el issue.
3. Seguí las instrucciones de [CONTRIBUTING.md](CONTRIBUTING.md).

Si tenés ideas para nuevos perfiles o áreas que no están listadas acá, abrí un issue con la etiqueta `roadmap-proposal` y lo discutimos con la comunidad.

---

> Este roadmap es un documento vivo. Se actualiza con cada release y con el aporte de la comunidad.
