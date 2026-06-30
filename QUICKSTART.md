# Guía de inicio rápido — check-legal-saas-ar

Tiempo estimado para tener el perfil funcionando: **5 minutos**.

---

## Paso 1: Cloná el repositorio (o descargá el archivo)

```bash
git clone https://github.com/ezebc182/check-legal-saas-ar.git
cd check-legal-saas-ar
```

El archivo principal que vas a usar es:

```
argentina/saas-CLAUDE.md
```

---

## Paso 2: Elegí tu camino de integración

Hay tres formas de activar el perfil según el entorno que uses.

---

### Camino A — Claude.ai Projects (recomendado para no técnicos)

1. Ingresá a [claude.ai](https://claude.ai) y creá un nuevo **Project**.
2. En la sección **Project Knowledge**, hacé clic en "Add content".
3. Subí el archivo `argentina/saas-CLAUDE.md` como documento de conocimiento.
4. (Opcional) Agregá también el archivo específico de tu área si existiera (ej.: `argentina/transito-CLAUDE.md`).
5. Iniciá una conversación dentro del Project.

El perfil estará activo para todas las conversaciones dentro de ese Project. No necesitás pegar nada manualmente.

---

### Camino B — Claude Code o Claude Desktop con CLAUDE.md

Si usás Claude Code (CLI) o Claude Desktop con soporte de proyecto local:

1. Cloná el repositorio en tu máquina (Paso 1).
2. Abrí o creá el archivo `CLAUDE.md` en la raíz de tu proyecto de trabajo.
3. Agregá esta línea al inicio del archivo:

```markdown
# Perfil legal activo

@/ruta/absoluta/a/check-legal-saas-ar/argentina/saas-CLAUDE.md
```

Reemplazá `/ruta/absoluta/a/` con el path real en tu sistema. Ejemplo en macOS:

```markdown
@/Users/tu-usuario/dev/check-legal-saas-ar/argentina/saas-CLAUDE.md
```

4. Claude Code cargará el perfil automáticamente al iniciar en ese directorio.

---

### Camino C — Cualquier modelo o interfaz (system prompt)

Si usás otra interfaz (ChatGPT, Gemini, API directa, Open WebUI, etc.):

1. Abrí el archivo `argentina/saas-CLAUDE.md` en cualquier editor de texto.
2. Copiá todo el contenido.
3. Pegalo como **system prompt** o **instrucciones del sistema** en la interfaz que uses.

Funciona con cualquier modelo de lenguaje con soporte de instrucciones del sistema.

---

## Paso 3: Configurá el contexto de tu empresa

Una vez activado el perfil, iniciá la sesión con el siguiente bloque de configuración. Reemplazá los valores entre corchetes con los datos reales de tu empresa:

```
CONFIGURACIÓN INICIAL DE CONTEXTO

MODELO_NEGOCIO: [B2B / B2C / B2B2C — describí brevemente qué vendés y a quién]
DATOS_TRATADOS: [qué tipos de datos personales tratás: nombre, email, IP, datos de uso, datos de pago, datos sensibles, etc.]
TRANSFERENCIAS_INTERNACIONALES: [¿tus datos salen de Argentina? ¿A qué países o proveedores? Ej.: AWS us-east-1, Google Workspace, Stripe]
JURISDICCION_CLIENTES: [¿tus clientes son solo argentinos o también del exterior? Mencionar países si aplica]
ETAPA_LEGAL: [¿ya tenés TyC y Política de Privacidad? ¿Estás inscripto en el RNBD de la AAIP? ¿Tenés contratos B2B firmados?]
```

Ejemplo completo para una SaaS B2B:

```
CONFIGURACIÓN INICIAL DE CONTEXTO

MODELO_NEGOCIO: SaaS B2B de gestión de inventario para PyMEs manufactureras argentinas. Plan mensual por usuario.
DATOS_TRATADOS: Nombre y email de usuarios, datos de empresa (CUIT, razón social), datos de uso de la plataforma (logs, acciones), no tratamos datos sensibles ni datos de pago (usamos Stripe como procesador).
TRANSFERENCIAS_INTERNACIONALES: Infraestructura en AWS us-east-1 (Virginia). Usamos Intercom para soporte, SendGrid para emails transaccionales, y Stripe para pagos.
JURISDICCION_CLIENTES: Clientes solo en Argentina por ahora. Expandión a Chile y Uruguay planificada para Q3 2026.
ETAPA_LEGAL: Tenemos TyC y Política de Privacidad desactualizadas (2022). No estamos inscriptos en el RNBD. No tenemos DPA firmado con AWS ni con los demás proveedores.
```

---

## Paso 4: Verificá que el perfil está activo

Hacé estas 3 consultas de prueba en orden. Si el perfil está correctamente activo, las respuestas van a incluir referencias normativas específicas de Argentina:

**Prueba 1 — Ley 25.326:**
```
¿Estamos obligados a inscribir nuestra base de datos de usuarios en el RNBD de la AAIP? ¿Cuál es el procedimiento y qué pasa si no lo hacemos?
```
Respuesta esperada: debe mencionar el art. 21 de la Ley 25.326, la Disposición AAIP 2/2020, el proceso online de registro y las sanciones del art. 31.

**Prueba 2 — Transferencias internacionales:**
```
Dado que nuestra infraestructura está en AWS us-east-1, ¿eso constituye una transferencia internacional de datos personales? ¿Qué obligaciones nos genera?
```
Respuesta esperada: debe mencionar el art. 12 de la Ley 25.326, el concepto de "nivel adecuado de protección", y la situación particular de EE.UU. bajo la normativa argentina.

**Prueba 3 — Propiedad intelectual:**
```
Dos de nuestros desarrolladores renunciaron y quieren usar el código que escribieron para nosotros en su propia startup. ¿El código es de ellos o de la empresa?
```
Respuesta esperada: debe mencionar el art. 4 de la Ley 11.723, la distinción entre relación de dependencia y contrato de locación de obra, y la importancia de las cláusulas contractuales.

---

## Paso 5: Empezá a trabajar

Con el perfil activo y el contexto cargado, podés hacer consultas directas como:

- "Necesito redactar una cláusula de confidencialidad para nuestro contrato B2B. ¿Qué debe incluir según la Ley 24.766?"
- "Un cliente de EEUU nos pide firmar un DPA. ¿Qué cláusulas son incompatibles con la Ley 25.326?"
- "¿Qué información es obligatorio incluir en la Política de Privacidad según la normativa argentina?"
- "Queremos registrar nuestra marca. ¿En qué clases de Niza tenemos que presentar la solicitud en el INPI?"

---

## Necesitás ayuda

- **Errores en el perfil**: abrí un [issue en GitHub](https://github.com/ezebc182/check-legal-saas-ar/issues)
- **Problemas de alto impacto**: mirá la [política de seguridad](SECURITY.md)
- **Contribuciones**: leé la [guía de contribución](CONTRIBUTING.md)

---

> **Recordatorio**: Este perfil es una herramienta de referencia y no reemplaza el asesoramiento de un abogado habilitado. Ante situaciones complejas o de alto impacto económico, consultá con un profesional del derecho.
