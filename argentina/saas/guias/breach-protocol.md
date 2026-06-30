# Protocolo de incidente de seguridad (breach) — SaaS argentino

> Marco normativo: Ley 25.326 [VERIFICAR VIGENCIA] no establece plazo expreso de notificación ante la AAIP. La Disposición AAIP 47/2018 [VERIFICAR VIGENCIA] exige procedimientos documentados de gestión de incidentes. Se recomienda seguir la práctica de 72 horas del GDPR como estándar de la industria aunque hoy no sea obligatorio legalmente en Argentina. [VERIFICAR VIGENCIA: si la reforma de la Ley 25.326 fue sancionada, los plazos de notificación pueden ser obligatorios — revisar antes de implementar este protocolo]

Este documento es el protocolo operativo a ejecutar cuando se detecta o sospecha un incidente de seguridad que pudo comprometer datos personales de titulares. Tenerlo definido antes de que ocurra un incidente reduce el tiempo de respuesta y mejora la calidad de las decisiones bajo presión.

---

## Paso 1 — Detección y contención (primeras 2 horas)

**Objetivo**: parar el daño activo y preservar la evidencia.

- [ ] Identificar el sistema o componente afectado
- [ ] Aislar el sistema si es técnicamente posible sin interrumpir el servicio completo (ej.: deshabilitar credenciales comprometidas, revocar API keys, bloquear IP atacante)
- [ ] **Preservar evidencia ANTES de cualquier acción de remediación**: exportar y guardar en almacenamiento seguro los logs del sistema, snapshots del estado del servidor o base de datos, capturas de red si están disponibles
- [ ] [RED FLAG] NO borrar, sobrescribir ni truncar logs antes de analizar — esto destruye la única evidencia del alcance real del incidente
- [ ] Identificar el vector de ataque tentativo: ¿brecha en una dependencia?, ¿credenciales filtradas?, ¿SQL injection?, ¿configuración incorrecta de bucket/storage?, ¿insider?
- [ ] Escalar inmediatamente a: responsable técnico senior, área legal o asesor legal externo, dirección ejecutiva
- [ ] Abrir un canal de comunicación interno dedicado al incidente (canal de Slack privado, sala de videollamada, hilo de email cerrado) — no usar canales públicos ni mencionar el incidente en canales abiertos hasta tener el alcance claro

---

## Paso 2 — Evaluación del impacto (primeras 4 horas)

**Objetivo**: entender qué pasó realmente antes de comunicar nada externamente.

- [ ] **Categoría de datos expuestos**:
  - Datos comunes: nombre, email, teléfono, dirección, historial de uso
  - Datos sensibles (art. 2 Ley 25.326 [VERIFICAR VIGENCIA]): datos de salud, ideología política, vida sexual, origen racial, convicciones religiosas, antecedentes penales
  - Credenciales de acceso: contraseñas (¿hasheadas? ¿en texto plano? ¿con qué algoritmo?), tokens, API keys
  - Datos financieros: números de tarjeta, CBU, datos bancarios

- [ ] **Número de titulares afectados**: estimación inicial con rango mínimo/máximo basado en el alcance del sistema comprometido

- [ ] **Naturaleza del incidente**:
  - Acceso no autorizado sin evidencia de exfiltración
  - Exfiltración confirmada (datos salieron del sistema)
  - Modificación o destrucción de datos
  - Ransomware: los datos fueron cifrados por el atacante

- [ ] **¿Los datos estaban cifrados?**: si sí, ¿fue comprometida la clave de cifrado? El cifrado efectivo reduce significativamente el riesgo real para los titulares incluso si los datos fueron exfiltrados

- [ ] **Clasificación del riesgo para los titulares**:
  - **Bajo**: datos genéricos, sin información de identificación directa, sin credenciales
  - **Medio**: emails y contraseñas hasheadas con algoritmo fuerte (bcrypt, argon2), datos de uso del producto sin información sensible
  - **Alto**: credenciales en texto plano o con hashing débil (MD5, SHA1), datos de salud, datos financieros completos, combinación de datos que permite robo de identidad

---

## Paso 3 — Decisión de notificación (primeras 8 horas)

**Objetivo**: decidir a quién notificar y cuándo. Esta decisión se toma con asesor legal.

- [ ] **¿Hay DPA firmados con clientes empresariales?**
  - Revisar el plazo de notificación acordado en cada DPA — el plazo contractual es vinculante independientemente del marco legal
  - Si el DPA dice 72 horas desde la detección, ese es el plazo máximo para notificar al cliente
  - Si el DPA dice 24 horas, ese es el plazo

- [ ] **Evaluación de notificación a la AAIP**:
  - Práctica recomendada: notificar dentro de las 72 horas si el incidente involucra datos personales y hay riesgo para los titulares
  - [VERIFICAR VIGENCIA: con la reforma de la Ley 25.326, puede ser obligatorio — verificar estado de la norma al momento del incidente]
  - Contacto AAIP: argentina.gob.ar/aaip [VERIFICAR VIGENCIA: canal oficial de reporte de brechas]

- [ ] **Evaluación de notificación directa a titulares afectados**:
  - Obligatorio si el riesgo clasificado es ALTO
  - Recomendado si el riesgo es MEDIO con datos sensibles involucrados
  - El principio rector: si vos fueses el titular, ¿quisieras saberlo para protegerte?

- [ ] **[RED FLAG] No comunicar externamente sin consultar al asesor legal primero** — la forma en que se comunica el incidente tiene consecuencias legales y reputacionales que una comunicación mal redactada puede agravar

---

## Paso 4 — Notificación a clientes empresariales (dentro de las 72 horas desde detección)

**Objetivo**: cumplir la obligación contractual del DPA y dar al cliente información suficiente para tomar decisiones.

- [ ] **Canal**: email al contacto de seguridad o legal del cliente, con copia al ejecutivo de cuenta
- [ ] **Asunto sugerido**: "Notificación de incidente de seguridad — [nombre del SaaS] — [fecha]"

**Contenido mínimo de la notificación**:

1. Qué ocurrió: descripción breve del incidente (sin detalles técnicos del vector de ataque en esta etapa)
2. Cuándo se detectó: fecha y hora de la detección inicial
3. Qué datos del cliente fueron afectados: si se sabe, qué registros del cliente puntualmente
4. Qué acciones se tomaron inmediatamente: contención, preservación de evidencia
5. Pasos siguientes: investigación en curso, plazo estimado para informe completo
6. Canal de consultas: nombre y email del contacto de seguridad del SaaS

- [ ] [RED FLAG] No incluir en la notificación inicial los detalles técnicos del vector de ataque ni las vulnerabilidades específicas — esa información puede ampliar el alcance del daño si la notificación se filtra o es interceptada

---

## Paso 5 — Notificación a la AAIP (práctica recomendada, dentro de las 72 horas)

**Objetivo**: cumplir con la práctica recomendada y, si la norma fue reformada, con la obligación legal.

- [ ] Verificar el canal oficial de reporte en argentina.gob.ar/aaip [VERIFICAR VIGENCIA]
- [ ] Preparar la notificación con asistencia del asesor legal

**Información a incluir en el reporte a la AAIP**:

1. Descripción del incidente: cuándo ocurrió (si se sabe), cuándo se detectó, naturaleza del incidente
2. Datos personales afectados: categorías de datos, estimación del número de titulares
3. Consecuencias probables: riesgo identificado para los titulares
4. Medidas adoptadas o en curso: contención, investigación, medidas de mitigación para los titulares
5. Contacto del responsable de protección de datos del SaaS

---

## Paso 6 — Notificación directa a titulares afectados (si hay riesgo ALTO)

**Objetivo**: dar a los titulares la información que necesitan para protegerse.

- [ ] Canal: email directo a cada titular afectado identificado
- [ ] Remitente: dirección conocida del SaaS (no una dirección nueva que parezca phishing)
- [ ] Asunto sugerido: "Aviso de seguridad importante sobre tu cuenta en [nombre del SaaS]"

**Contenido obligatorio**:

1. Qué información fue expuesta: ser específico — "tu email y contraseña hasheada" o "tu nombre y dirección de facturación"
2. Qué riesgo implica para el titular: qué puede hacer un tercero con esa información
3. Qué puede hacer el titular para protegerse:
   - Cambiar la contraseña de [nombre del SaaS] inmediatamente
   - Cambiar la misma contraseña en cualquier otro servicio donde la usara
   - Habilitar autenticación de dos factores si está disponible
   - Monitorear movimientos inusuales en cuentas bancarias si hubo datos financieros involucrados
4. Qué está haciendo el SaaS: resumen de las medidas tomadas
5. Canal de consultas: email de contacto con tiempo de respuesta comprometido

- [ ] [RED FLAG] No minimizar el incidente, no usar eufemismos como "evento de seguridad menor" si el riesgo es real, no dar información falsa sobre el alcance — una notificación honesta protege mejor al titular y reduce la responsabilidad legal

---

## Paso 7 — Documentación y post-mortem (dentro de los 30 días)

**Objetivo**: dejar registro para cumplimiento normativo y prevenir recurrencia.

- [ ] **Documento de cronología del incidente** (uso interno):
  - Línea de tiempo: cuándo ocurrió el incidente, cuándo fue detectado, cuándo se tomó cada medida
  - Causa raíz identificada
  - Sistemas y datos afectados con detalle
  - Lista de titulares notificados y fecha de notificación
  - Respuestas de clientes empresariales y consultas recibidas de titulares
  - Este documento puede ser requerido por la AAIP en una inspección — guardarlo con acceso restringido

- [ ] **Actualización del inventario de riesgos**: incorporar el incidente como caso de referencia y actualizar la valoración del riesgo del sistema afectado

- [ ] **Revisión de medidas de seguridad**:
  - ¿Qué control falló o estaba ausente?
  - ¿Qué medida hubiera detectado el incidente antes?
  - ¿Qué medida hubiera contenido el daño?
  - Implementar las medidas correctivas y dejar registro de implementación

- [ ] **Revisión de contratos con terceros si el incidente involucró a un proveedor**:
  - ¿El DPA con ese proveedor cubre el incidente ocurrido?
  - ¿El proveedor notificó en el plazo acordado?
  - ¿Hay base para reclamo contractual contra el proveedor?
  - Consultar al asesor legal antes de cualquier comunicación al proveedor sobre responsabilidad
