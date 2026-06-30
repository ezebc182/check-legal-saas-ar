# Guía de contribución — check-legal-saas-ar

Gracias por contribuir. Este repo es un recurso para equipos de SaaS argentinas que necesitan entender el marco legal local. La calidad del contenido importa: una referencia normativa incorrecta puede inducir a error a alguien que tome decisiones reales.

> **Aviso**: Este repositorio tiene fines informativos. No constituye asesoramiento jurídico. Ante dudas concretas, consultá con un abogado matriculado.

---

## Qué tipo de contribuciones se aceptan

| Tipo | Aceptado | Notas |
|------|----------|-------|
| Corrección de referencia normativa incorrecta | ✅ | Requiere fuente oficial |
| Actualización de norma derogada o modificada | ✅ | Requiere fuente oficial + fecha |
| Nuevo perfil de área legal | ✅ | Abrí un issue primero para discutir el alcance |
| Nuevo modelo de contrato o cláusula | ✅ | Debe seguir la estructura existente |
| Corrección de vocabulario (GDPR → terminología Ley 25.326) | ✅ | Ver estándares más abajo |
| Opinión jurídica sobre qué es legal o ilegal | ❌ | El repo informa, no asesora |
| Contenido sobre legislación extranjera sin contexto argentino | ❌ | Fuera de scope |
| Links a fuentes secundarias como único respaldo | ❌ | Solo fuentes oficiales |

---

## Cómo proponer un cambio

### 1. Abrí un issue primero (para cambios no triviales)

Antes de escribir código o contenido, abrí un issue usando el template correspondiente:

- **Error en perfil legal** → referencia incorrecta, marcador faltante, red flag errónea
- **Normativa desactualizada** → ley reformada, disposición derogada
- **Solicitud de nuevo perfil** → área legal sin cobertura actual

Para correcciones menores (typo, link roto, error de formato), podés ir directo al PR.

### 2. Forkear el repo y crear una rama

```bash
git clone https://github.com/TU-USUARIO/check-legal-saas-ar.git
cd check-legal-saas-ar
git checkout -b fix/nombre-descriptivo-del-cambio
```

Convenciones de nombre de rama:

| Tipo de cambio | Prefijo |
|----------------|---------|
| Corrección normativa | `fix/` |
| Norma desactualizada | `update/` |
| Nuevo perfil | `feat/` |
| Nuevo contrato/cláusula | `feat/` |
| Documentación del repo | `docs/` |

### 3. Hacé los cambios respetando los estándares de calidad

Ver sección **Estándares de calidad** más abajo.

### 4. Abrí el Pull Request

Usá el template de PR que aparece automáticamente al abrir un PR. Completá todas las secciones, especialmente las normas verificadas y el checklist.

---

## Estándares de calidad

### Vocabulario obligatorio — Ley 25.326 argentina

Este repo usa terminología de la **Ley 25.326 de Protección de los Datos Personales** y sus normas complementarias. **No usar terminología GDPR** salvo en secciones que explícitamente comparen ambos regímenes.

| ❌ No usar (GDPR / genérico) | ✅ Usar (Ley 25.326) |
|------------------------------|----------------------|
| datos personales sensibles | datos sensibles (art. 2, Ley 25.326) |
| responsable del tratamiento | responsable del archivo / responsable del banco de datos |
| encargado del tratamiento | usuario del banco de datos |
| interesado | titular de los datos |
| base legal del tratamiento | supuesto de legitimación (art. 5, Ley 25.326) |
| derecho al olvido | derecho de supresión (art. 16, Ley 25.326) |
| Autoridad de control | AAIP (Agencia de Acceso a la Información Pública) |
| DPO / Data Protection Officer | No existe figura equivalente obligatoria en la Ley 25.326 actual |

### Marcadores obligatorios

Usá `[VERIFICAR VIGENCIA]` en cualquier referencia normativa que:

- Esté sujeta a reglamentación pendiente
- Haya sido modificada recientemente (últimos 24 meses)
- Tenga interpretación controvertida por parte de la AAIP u otros organismos
- Sea un proyecto de ley o disposición en proceso de aprobación

Ejemplo correcto:

```markdown
El art. 26 de la Ley 25.326 regula la prestación de servicios de información crediticia.
**[VERIFICAR VIGENCIA]** — Existe un anteproyecto de reforma integral de la LPDP en circulación
desde 2023. Verificar estado en https://www.argentina.gob.ar/aaip antes de aplicar.
```

### El repo informa, no asesora

Los perfiles deben describir el marco normativo, no prescribir conductas. Evitá:

- "Debés registrar tu base de datos en la AAIP" → "La Ley 25.326 establece la obligación de inscripción de bases de datos (art. 21). Verificar con asesor legal el alcance aplicable a tu caso."
- "Esto es ilegal" → "Esta práctica puede constituir infracción al art. X de la Ley Y. Consultar con abogado."
- "Podés hacer X sin problemas" → nunca dar certeza jurídica en el repo

---

## Cómo verificar normativa

### Fuentes oficiales — por área

**Protección de datos personales (Ley 25.326)**
- AAIP: https://www.argentina.gob.ar/aaip
- InfoLEG — Ley 25.326: https://www.infoleg.gob.ar/infolegInternet/anexos/60000-64999/64790/norma.htm
- InfoLEG — Decreto 1558/2001: https://www.infoleg.gob.ar/infolegInternet/anexos/70000-74999/70368/norma.htm

**Normativa general**
- InfoLEG (base de datos oficial de legislación nacional): https://www.infoleg.gob.ar/
- Boletín Oficial de la República Argentina: https://www.boletinoficial.gob.ar/

**Propiedad intelectual / Software**
- INPI (Instituto Nacional de la Propiedad Industrial): https://www.inpi.gob.ar/
- InfoLEG — Ley 11.723 (Propiedad Intelectual): https://www.infoleg.gob.ar/

**Defensa del consumidor**
- Secretaría de Comercio: https://www.argentina.gob.ar/produccion/defensadelconsumidor
- InfoLEG — Ley 24.240: https://www.infoleg.gob.ar/

**Defensa de la competencia**
- CNDC (Comisión Nacional de Defensa de la Competencia): https://www.argentina.gob.ar/cndc
- InfoLEG — Ley 27.442: https://www.infoleg.gob.ar/

**Comercio electrónico**
- InfoLEG — Ley 25.065 (tarjetas) y Resolución SCT relevantes

**Tributario / Facturación electrónica**
- AFIP: https://www.afip.gob.ar/
- InfoLEG — normas tributarias

### Cómo buscar en InfoLEG

1. Ingresá a https://www.infoleg.gob.ar/
2. Usá el número de norma o palabras clave en el buscador
3. Verificá la **fecha de última actualización** y si hay normas modificatorias
4. Si la norma tiene modificaciones, revisá el texto consolidado

---

## Proceso de review

1. Todo PR requiere revisión de al menos un maintainer (@ezebc182)
2. Los PRs con cambios normativos deben incluir la URL de InfoLEG o fuente oficial en la descripción
3. Si hay dudas sobre la interpretación de una norma, se puede solicitar una segunda opinión antes de mergear
4. El review puede incluir pedidos de aclaración o corrección — respondé en los comentarios del PR, no en un nuevo issue
5. Una vez aprobado, el maintainer hace el merge

### Tiempo estimado de review

- Correcciones menores (typo, formato): 2-5 días hábiles
- Correcciones normativas: 5-10 días hábiles (requiere verificación independiente)
- Nuevos perfiles: 10-20 días hábiles (alcance y calidad a verificar)

---

## Licencia de las contribuciones

Al contribuir a este repositorio, aceptás que tu contribución se licencie bajo **Apache 2.0**, la misma licencia del proyecto. Ver [LICENSE](./LICENSE).

---

## Preguntas frecuentes

**¿Puedo contribuir si no soy abogado?**
Sí. Podés reportar errores, proponer mejoras de formato, actualizar links rotos, o señalar normativa desactualizada citando la fuente oficial. La validación jurídica del contenido sustantivo queda a cargo del review.

**¿Qué pasa si no encuentro la norma en InfoLEG?**
Indicalo en el issue o PR. Algunas disposiciones de organismos (AAIP, BCRA, AFIP) no están en InfoLEG pero sí en el sitio del organismo correspondiente. Usá esas fuentes oficiales directas.

**¿Se aceptan traducciones al inglés de los perfiles?**
Por ahora no está en el scope. El repo es específico del marco legal argentino y el público objetivo opera en español.

**¿Puedo referenciar jurisprudencia?**
Sí, como contexto complementario, pero no como fuente primaria para afirmaciones normativas. La jurisprudencia ilustra interpretación; la norma es la fuente.
