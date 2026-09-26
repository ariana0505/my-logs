Fecha : 25/09/26

# Creando un proyecto, entendiendo el contexto y la memoria

---

## Objetivos de la clase 🎯

---

## `/context`

El comando `/context` muestra un desglose de cómo está ocupada la ventana de contexto en ese momento, es decir, en qué se está gastando el límite de tokens.

La salida se ve como una barra o lista con categorías, cada una con su porcentaje o cantidad de tokens:

- **System prompt**: las instrucciones base con las que opera Claude Code, incluyendo el harness y las reglas del entorno.
- **System tools**: la definición de las herramientas disponibles (`Bash`, `Edit`, `Write`, etc.), que ocupa espacio aunque no se usen todas.
- **MCP tools**: si hay servidores MCP conectados, sus definiciones también consumen contexto, incluso sin haberlos usado.
- **Memory files**: el contenido cargado desde `CLAUDE.md` en sus distintos scopes.
- **Messages**: todo el historial de la conversación actual, mensajes y respuestas.
- **Free space / disponible**: cuánto queda antes de llegar al límite.

### Para qué sirve

Ayuda a diagnosticar por qué una sesión se siente «llena» o por qué el modelo empieza a resumir o perder detalle, y a decidir si conviene desconectar MCPs que no se necesitan, acortar un `CLAUDE.md` muy largo, o abrir una sesión nueva.

### Caso real: carpeta recién creada («Albumcito Facilito») ya muestra espacio ocupado

Ejemplo de salida real de `/context` en una carpeta recién creada, sin archivos de proyecto todavía:

```
Sonnet 5 — claude-sonnet-5 — 38.8k/1m tokens (4%)

Estimated usage by category
System prompt: 8.9k tokens (0.9%)
System tools: 19.4k tokens (1.9%)
MCP tools: 640 tokens (0.1%)
Skills: 9.9k tokens (1.0%)
Messages: 8 tokens (0.0%)
Free space: 928.2k tokens (92.8%)
Autocompact buffer: 33k tokens (3.3%)

MCP tools · /mcp (loaded on-demand) → 130 tools · 640 tokens
Skills · /skills → 82 skills · 9.9k tokens
```

**Por qué aparece espacio ocupado aunque la carpeta esté vacía:** lo ocupado no son archivos del proyecto (eso entraría en «Messages», que aquí es de apenas 8 tokens, casi nada). Es el costo fijo que trae cada sesión nueva de Claude Code, sin importar si la carpeta tiene contenido:

- **System prompt**: instrucciones base del propio Claude Code, siempre presentes.
- **System tools**: las definiciones de `Bash`, `Edit`, `Write`, etc., existen aunque no se hayan usado.
- **MCP tools**: si hay servidores MCP configurados a nivel de cuenta o sistema (Gmail, Notion, etc.), sus definiciones se cargan igual, aunque el proyecto sea nuevo.
- **Skills**: la lista de skills disponibles también se carga de entrada, sin haber invocado ninguna.

Conclusión: no es que la carpeta «ya tenga espacio ocupado» por contenido propio; Claude Code siempre carga cierto equipaje fijo —sus propias instrucciones, la definición de herramientas, y todos los MCPs y skills configurados en el entorno— antes de escribir el primer mensaje. Ese 4% de uso es overhead del sistema, no del proyecto.

---

## ⚠️ Importante recordar: para qué sirve crear un `CLAUDE.md` en cada proyecto

Un `CLAUDE.md` en cada proyecto sirve para no tener que explicarle a Claude Code, desde cero, cada vez que se abre una sesión nueva, cosas que ya se saben del propio proyecto. Es memoria persistente a nivel Project, así que se carga automáticamente al inicio de cualquier sesión que se abra en esa carpeta.

Ejemplos:

- **Registro de pagos por Yape (Charter P1)**: sin `CLAUDE.md`, cada sesión nueva habría que repetir «esto es para mi abuela Celia, quien administra un minimarket, el alcance no incluye conexión con Yape ni notificaciones, uso GitHub Actions para CI». Con `CLAUDE.md`, se escribe una sola vez y queda presente desde el primer mensaje de cada sesión futura.
- **Albumcito Facilito**: anotar que el proyecto usa un monorepo con Turborepo, backend en NestJS y frontend en Next.js. Así, en una sesión nueva, al pedir «agrega un endpoint», Claude Code ya sabe que debe usar NestJS sin repetírselo.

En concreto, sirve para tres cosas:

- **Evitar repetición.** Reglas, contexto de negocio, decisiones ya tomadas, quedan escritas una vez y se reutilizan en cada sesión.
- **Consistencia entre sesiones y personas.** Si el proyecto se comparte con alguien más (por ejemplo al subir el repo a GitHub), esa persona también hereda el mismo contexto al usar Claude Code ahí, porque el scope Project se comparte con el equipo.
- **Guiar el estilo de trabajo.** Se pueden anotar convenciones propias, como «usa nombres de variables en español» o «no toques la carpeta de configuración sin preguntar», y Claude Code las respeta desde el inicio.

**Diferencia clave**: los archivos de contenido normales (como estos logs de `ClaudeCodeCourse`) solo se leen cuando se pide explícitamente. Un `CLAUDE.md` se carga automáticamente sin pedirlo, en cada sesión nueva de esa carpeta.
