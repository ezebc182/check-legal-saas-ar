# Política de Seguridad — check-legal-saas-ar

## Alcance

Este repositorio no contiene código ejecutable. Los "problemas de seguridad" en este contexto se refieren a **errores normativos en los perfiles de práctica legal** que puedan inducir a un operador SaaS a tomar decisiones que le causen perjuicio legal, regulatorio o económico.

---

## Tipos de problemas y cómo reportarlos

### Vía issue público (GitHub Issues)

Usá un issue público para reportar **errores normativos de bajo riesgo**, como:

- Cita incorrecta de un artículo de la Ley 25.326, Ley 11.723, Ley 24.766, Ley 22.362, LDC o CCCN
- Referencia a una resolución de la AAIP que fue modificada o derogada
- Interpretación doctrinaria minoritaria presentada como mayoritaria sin aclaración
- Ejemplo o caso de uso que no refleja fielmente el marco normativo vigente
- Falta de mención de obligaciones formales aplicables (ej.: inscripción RNBD, DPO, etc.)
- Actualización normativa que deja desactualizado un apartado del perfil

Para abrir un issue, usá la plantilla **"Error normativo"** y completá:
1. Sección y párrafo específico donde se encuentra el error
2. Texto actual (cita textual)
3. Normativa o fuente que contradice o corrige el contenido
4. Texto propuesto o corrección sugerida

### Vía email privado (problemas de alto impacto)

Enviá un email a **jetamclain@gmail.com** con asunto `[SECURITY] check-legal-saas-ar` cuando el problema sea de **alto impacto potencial**, es decir, cuando el perfil:

- Aconseje activamente una conducta que constituya infracción a la Ley 25.326 o normativa concordante
- Induzca a omitir una obligación cuyo incumplimiento acarree sanciones de la AAIP o de organismos reguladores
- Contenga una recomendación que, si se sigue de buena fe, podría generar responsabilidad civil o penal para el operador
- Sugiera cláusulas contractuales nulas de pleno derecho bajo el CCCN o la LDC
- Exponga datos personales de titulares de manera indirecta (ej.: ejemplos con datos reales)

El email debe incluir:
1. Descripción del problema (sección, cita textual)
2. Normativa, jurisprudencia o doctrina que fundamenta el error
3. Impacto potencial estimado (quién podría verse perjudicado y cómo)
4. Propuesta de corrección si la tenés disponible

Nos comprometemos a responder en un plazo de **5 días hábiles** y a publicar una corrección dentro de los **15 días hábiles** de confirmado el error.

---

## Versiones con soporte activo

| Versión | Estado          |
|---------|-----------------|
| 1.x     | Con soporte activo |
| < 1.0   | Sin soporte     |

---

## Reconocimiento

Los colaboradores que reporten errores verificados serán mencionados en el CHANGELOG correspondiente a la corrección, salvo que soliciten anonimato.

---

## Aviso legal (disclaimer)

> **IMPORTANTE:** El contenido de este repositorio —incluyendo los perfiles de práctica, ejemplos, plantillas y guías— constituye **información de referencia general** y **no constituye asesoramiento jurídico** de ningún tipo.
>
> El uso de estos perfiles no genera relación abogado-cliente entre los mantenedores y los usuarios del repositorio. Cada situación concreta requiere el análisis de un profesional del derecho habilitado en la República Argentina.
>
> Los mantenedores no asumen responsabilidad por decisiones tomadas con base exclusiva en el contenido de este repositorio. Ante dudas, consultá a un abogado especializado.
