# Checklist: Privacy Policy para SaaS argentino
## Marco normativo: Ley 25.326 de Protección de Datos Personales

---

> **ADVERTENCIA NORMATIVA CRÍTICA**
>
> La Ley 25.326 fue sancionada en el año 2000. Al 2026 **sigue vigente sin reforma sustancial**.
> Su vocabulario es distinto al del GDPR europeo. Usar términos del GDPR en un documento bajo
> jurisdicción argentina es un error técnico que puede invalidar cláusulas o generar confusión
> ante la AAIP. Usá SIEMPRE el vocabulario de la ley 25.326.
>
> La AAIP puede iniciar actuaciones de oficio. El incumplimiento del art. 6 (información al
> titular) habilita sanciones que van desde el apercibimiento hasta la clausura de la base
> de datos (art. 31 Ley 25.326) [VERIFICAR VIGENCIA: Ley 25.326 art. 31].

---

## Tabla de vocabulario obligatorio

| Término GDPR (NO usar) | Término Ley 25.326 (usar esto) | Artículo de referencia |
|---|---|---|
| Data controller | Responsable del archivo / Responsable del tratamiento | Art. 2 Ley 25.326 |
| Data processor | Usuario del dato | Art. 2 Ley 25.326 |
| Data subject | Titular del dato | Art. 2 Ley 25.326 |
| DPO (Data Protection Officer) | No existe figura obligatoria bajo ley vigente | — |
| Right to erasure | Derecho de supresión | Art. 16 Ley 25.326 |
| Right to access | Derecho de acceso | Art. 14 Ley 25.326 |
| Right to rectification | Derecho de rectificación y actualización | Art. 16 Ley 25.326 |
| Data portability | No contemplado en la ley vigente | — |
| Lawful basis | No existe listado cerrado de bases legales como en GDPR. El consentimiento informado es la regla general (art. 5). Excepciones: art. 5 inc. 2 | Art. 5 Ley 25.326 |
| Sensitive data | Datos sensibles | Art. 2 y art. 7 Ley 25.326 |
| Processing | Tratamiento de datos | Art. 2 Ley 25.326 |
| Third-party transfer | Cesión / transferencia | Art. 11 y art. 12 Ley 25.326 |

---

## Checklist de CONTENIDO MÍNIMO OBLIGATORIO

Basado en el art. 6 Ley 25.326 (información al momento de recolección) y normativa complementaria [VERIFICAR VIGENCIA: Ley 25.326 art. 6].

### A. Identificación del responsable del archivo

- [ ] Nombre o razón social completa del responsable del archivo
- [ ] CUIT del responsable
- [ ] Domicilio físico en Argentina (calle, número, piso/depto, localidad, provincia, código postal)
- [ ] Si hay múltiples personas jurídicas involucradas (holding, subsidiaria que opera el SaaS), aclarar cuál es el responsable del archivo ante la AAIP
- [ ] Canal de contacto directo para ejercicio de derechos: dirección de email dedicada (no info@, no soporte@) y domicilio postal

### B. Finalidad del tratamiento

- [ ] Finalidad descripta en términos específicos y concretos (no "mejorar nuestros servicios" sin más detalle) [RED FLAG: finalidad genérica es ilegítima bajo art. 4 Ley 25.326]
- [ ] Si hay más de una finalidad, cada una enumerada por separado
- [ ] Si la finalidad cambia después de la recolección: se debe informar y obtener nuevo consentimiento

### C. Destinatarios de los datos

- [ ] Terceros a quienes se ceden los datos (nombre o categoría del cesionario)
- [ ] Finalidad de la cesión
- [ ] Si se cede a proveedores de infraestructura (AWS, GCP, Azure, Cloudflare): mencionarlos como "usuarios del dato" o "encargados del tratamiento" según el rol real
- [ ] Si no hay cesión a terceros: declararlo expresamente

### D. Inscripción ante la AAIP

- [ ] Mención de la existencia de la base de datos [VERIFICAR VIGENCIA: art. 21 Ley 25.326]
- [ ] Número de inscripción ante el Registro Nacional de Bases de Datos de la AAIP
- [ ] Si la inscripción está en trámite: indicarlo y actualizar el documento cuando se obtenga el número [RED FLAG: operar sin inscripción es infracción sancionable]

### E. Carácter de los datos

- [ ] Indicar qué datos son de suministro obligatorio para usar el servicio
- [ ] Indicar qué datos son opcionales
- [ ] Consecuencias de no proporcionar los datos obligatorios (ej: "sin nombre y email no podemos crear su cuenta")

### F. Derechos del titular del dato

- [ ] Derecho de acceso (art. 14 Ley 25.326): el titular puede solicitar qué datos tiene el responsable sobre él/ella [VERIFICAR VIGENCIA: Ley 25.326 art. 14]
- [ ] Derecho de rectificación: corrección de datos inexactos
- [ ] Derecho de actualización: actualización de datos incompletos u obsoletos
- [ ] Derecho de supresión (art. 16 Ley 25.326): eliminación de datos cuando corresponde [VERIFICAR VIGENCIA: Ley 25.326 art. 16]
- [ ] Derecho de confidencialidad: oposición al tratamiento en ciertos casos (art. 34 del dec. reglamentario 1558/2001) [VERIFICAR VIGENCIA: Decreto 1558/2001 art. 34]
- [ ] Plazo para responder al ejercicio de derechos: la ley establece 5 días hábiles para el acceso (art. 14) [VERIFICAR VIGENCIA: Ley 25.326 art. 14]
- [ ] Cómo ejercer cada derecho: instrucciones claras (email a enviar, datos a incluir en la solicitud)

### G. Datos sensibles (si aplica)

- [ ] Identificar si el SaaS trata datos sensibles: salud, vida sexual, origen racial o étnico, opiniones políticas, convicciones religiosas o morales, afiliación sindical (art. 2 y art. 7 Ley 25.326)
- [ ] Base legal específica del art. 7: el consentimiento general de los TyC NO es suficiente para datos sensibles; se requiere consentimiento expreso y por escrito [RED FLAG: crítico]
- [ ] Si el SaaS procesa datos de salud (app médica, bienestar, seguros): analizar art. 7 con especial cuidado antes de publicar

### H. Transferencias internacionales (si aplica)

- [ ] Si los datos se transfieren a servidores o entidades en el exterior: mencionarlo (art. 12 Ley 25.326) [VERIFICAR VIGENCIA: Ley 25.326 art. 12]
- [ ] País o países destinatarios de la transferencia
- [ ] Nivel de protección del país destinatario: la AAIP publica la lista de países con nivel adecuado [VERIFICAR VIGENCIA: resoluciones AAIP sobre nivel adecuado]
- [ ] Si el país no tiene nivel adecuado (ej: EE.UU. sin mecanismo de legitimación): identificar el mecanismo alternativo utilizado [RED FLAG: transferencia a EE.UU. sin mecanismo = riesgo art. 12]

---

## Checklist de RED FLAGS comunes en Privacy Policy de SaaS

Estos son los errores más frecuentes que encontramos en SaaS argentinos. Antes de publicar tu Privacy Policy, revisá cada uno.

- [ ] **Vocabulario GDPR en documento argentino**: ¿Usás "controlador de datos" en lugar de "responsable del archivo"? → cambiar todo el documento [RED FLAG]
- [ ] **Finalidad genérica**: ¿La finalidad dice "mejorar nuestros servicios", "personalizar la experiencia" o "fines estadísticos" sin más detalle? → demasiado vago, viola art. 4 Ley 25.326 [RED FLAG]
- [ ] **Sin mecanismo de ejercicio de derechos**: ¿No hay instrucciones claras para que el titular acceda, rectifique o suprima sus datos? → art. 14 y 16 incumplidos [RED FLAG crítico]
- [ ] **Transferencia a EE.UU. sin legitimación**: ¿Usás AWS us-east, Google Analytics, Stripe, Twilio o similares y no mencionás el mecanismo de legitimación para la transferencia internacional? → riesgo serio [RED FLAG]
- [ ] **Datos sensibles con consentimiento general**: ¿Tratás datos de salud, biometría o datos de menores bajo el consentimiento estándar de los TyC? → art. 7 requiere consentimiento expreso y diferenciado [RED FLAG crítico]
- [ ] **Sin número de inscripción AAIP**: ¿No mencionás el número de inscripción de tu base de datos ante la AAIP? → art. 21 incumplido [RED FLAG]
- [ ] **Domicilio fiscal inexistente o incorrecto**: ¿El domicilio del responsable del archivo no coincide con el registrado ante la AFIP? → inconsistencia documental
- [ ] **Plazo de retención ausente**: ¿No informás cuánto tiempo conservás los datos? → buena práctica, aunque no exigido expresamente por la ley vigente; recomendado para reducir riesgo
- [ ] **Link roto o documento desactualizado**: ¿La Privacy Policy tiene más de 2 años sin revisión? → verificar si hubo resoluciones AAIP que impacten el contenido

---

## Sección especial: usuarios en la Unión Europea

Si el SaaS tiene usuarios en la UE (aunque sea residualmente), el GDPR aplica de manera extraterritorial (art. 3 GDPR). Esto NO reemplaza la Ley 25.326 pero se adiciona.

Para cubrir usuarios en la UE mínimamente, agregar:

- Identificación del representante en la UE si corresponde (art. 27 GDPR) — solo obligatorio si hay procesamiento sistemático de personas en la UE
- Base legal GDPR para cada finalidad (consentimiento, contrato, interés legítimo, etc.) — distinto del régimen argentino
- Derechos adicionales del GDPR no contemplados en la ley argentina: portabilidad (art. 20 GDPR), oposición reforzada (art. 21 GDPR), decisiones automatizadas (art. 22 GDPR)
- Autoridad de control competente en la UE para reclamaciones (la AAIP no tiene jurisdicción sobre titulares en la UE)

**Importante**: Este párrafo es orientativo. El análisis completo de aplicabilidad del GDPR requiere evaluación caso por caso. No publicar una Privacy Policy "dual" (ley argentina + GDPR) sin revisión de un abogado con conocimiento de ambos marcos.

---

## Cómo usar el perfil de IA para auditar esta Privacy Policy

Una vez que cargaste el perfil `mcp-legal-ar` o el skill correspondiente de este repo, pasale al modelo el texto completo de tu Privacy Policy con esta instrucción:

```
Auditá esta Privacy Policy bajo Ley 25.326 argentina. Usá el checklist del archivo
`privacy-policy-checklist.md` como criterio. Para cada ítem del checklist, indicá:
- CUMPLE / NO CUMPLE / PARCIAL
- Cita textual del documento que justifica tu evaluación (o indicá si está ausente)
- Sugerencia de corrección si corresponde

Usá vocabulario Ley 25.326, no GDPR. Indicá [VERIFICAR VIGENCIA] donde las normas
citadas puedan haber cambiado. Señalá [RED FLAG] en problemas críticos.
```

El modelo va a devolver un informe estructurado por artículo, con citas textuales y sugerencias de corrección específicas.
