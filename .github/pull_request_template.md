# Pull Request

## Tipo de cambio

<!-- Marcá lo que corresponda. -->

- [ ] Corrección normativa (referencia incorrecta, artículo mal citado)
- [ ] Normativa desactualizada (ley reformada, disposición derogada)
- [ ] Nuevo perfil de área legal
- [ ] Nuevo modelo de contrato o cláusula
- [ ] Actualización de checklist existente
- [ ] Corrección de vocabulario o estilo
- [ ] Mejora estructural o de formato
- [ ] Documentación del repo (README, CONTRIBUTING, etc.)

## Issue vinculada

<!-- Todo PR debe referenciar un issue previo salvo cambios triviales de typo/formato. -->

Closes #

## Descripción del cambio

<!-- Explicá qué cambiaste y POR QUÉ. Un PR sin contexto demora el review. -->

## Normas verificadas

<!-- Listá las normas que tocaste y confirmá que verificaste su vigencia actual. -->

| Norma | Verificada en | Fecha de consulta |
|-------|---------------|------------------|
| | InfoLEG / AAIP / BO | |
| | | |

## Checklist de calidad

### Normativa y contenido

- [ ] Todas las referencias normativas incluyen número de ley/decreto/disposición y artículo específico
- [ ] Usé vocabulario de la Ley 25.326 argentina (NO terminología GDPR europea)
  - "datos personales sensibles" → "datos sensibles" (art. 2, Ley 25.326)
  - "responsable del tratamiento" → "responsable del archivo" o "responsable del banco de datos"
  - "interesado" → "titular de los datos"
  - "base legal" → "legitimación" o directamente el supuesto del art. 5
- [ ] Agregué marcador `[VERIFICAR VIGENCIA]` en toda norma con vigencia incierta o sujeta a reglamentación pendiente
- [ ] No incluí asesoramiento jurídico directo — el repo informa, no asesora
- [ ] No usé frases como "debés hacer X" o "esto es legal/ilegal" sin la advertencia correspondiente

### Formato y estructura

- [ ] El archivo sigue la estructura de los perfiles existentes (encabezado, secciones, marcadores)
- [ ] Los links a normas apuntan a InfoLEG, AAIP u organismos oficiales — no a blogs ni fuentes secundarias
- [ ] Si el perfil es nuevo, lo agregué al índice correspondiente (README o archivo de índice del área)

### Revisión propia

- [ ] Leí el archivo completo antes de abrir el PR
- [ ] El diff no incluye cambios accidentales en otros archivos
- [ ] Si modifiqué un modelo de contrato, verifiqué que las cláusulas sean coherentes entre sí

## Notas para el reviewer

<!-- Cualquier contexto que ayude al review: ambigüedades normativas, decisiones de diseño, áreas donde no estás seguro. -->
