# Funcionamiento de una sesión de trabajo

---

## Objetivos de la clase 🎯

Entender cómo Claude Code liga cada sesión de trabajo a una carpeta y qué significa esto en términos de jerarquía de directorios (padres e hijos).

---

## Sesión de trabajo

Al ejecutar el comando `claude` iniciamos una sesión de trabajo; en términos simples esta es una conversación.

Esta conversación tiene un contexto inicial, es un loop donde estamos interactuando constantemente con nuestro asistente/agente.

Cada sesión es independiente.

Mientras conversamos podemos hacer algunas cosas que pueden afectar cómo se lleva a cabo:

1. Modelos (`/model`)
2. Modos

---

## Sesión ligada a una carpeta

Cuando ejecuto `claude` en una carpeta, esa sesión queda asociada a esa ruta específica del disco, no a mi usuario en general.

- Si vuelvo a esa misma carpeta y ejecuto `claude` de nuevo, puede reanudar la conversación anterior porque el historial quedó guardado vinculado a esa ubicación.
- Si abro Claude Code en una carpeta distinta, es una sesión nueva y separada, aunque sea el mismo proyecto pero en otra ruta.

---

## Carpetas padre, hijas y hermanas

Se refiere a la jerarquía de directorios del sistema de archivos. Ejemplo:

```
Desktop/
└── Logs/                  ← carpeta padre
    ├── CharterP1/          ← carpeta hija
    └── ClaudeCodeCourse/   ← carpeta hija (y hermana de CharterP1)
```

- `Logs` es la carpeta **padre** de `CharterP1` y de `ClaudeCodeCourse`.
- `CharterP1` y `ClaudeCodeCourse` son **hermanas** entre sí, porque comparten el mismo padre.

### Por qué importa para el contexto

El contexto —como el archivo `CLAUDE.md`— se busca subiendo por las carpetas padre desde donde ejecuto la sesión.

- Si tengo un `CLAUDE.md` en `Desktop/Logs`, cualquier sesión que abra dentro de `CharterP1` o `ClaudeCodeCourse` puede heredar ese contexto porque están un nivel abajo (son hijas).
- Dos carpetas hermanas **no** comparten contexto entre sí automáticamente, aunque estén una al lado de la otra.

---

## Session continuity

`session-abc123`

`claude --continue` / `claude --resume` → appends to same session.

Fork creates a new session from any point:

`claude --resume abc123 --fork-session` → crea una nueva sesión (`session-xyz789`, new ID) a partir de un punto dado de la sesión original.

### En profundidad

La imagen muestra dos formas de manejar la continuidad de una sesión:

**1. Continuar la misma sesión (arriba).** Una sesión tiene un identificador, `session-abc123`, representado como una línea de puntos que avanza en el tiempo, donde cada punto es un mensaje o paso. Con `claude --continue` o `claude --resume` se siguen agregando puntos a esa misma línea; el identificador de sesión no cambia.

**2. Fork, crear una sesión nueva desde un punto anterior (abajo).** En vez de seguir agregando al final de la línea, se elige un punto intermedio de esa misma sesión original y desde ahí se abre una rama completamente nueva, con un identificador distinto (`session-xyz789`, new ID). El comando es `claude --resume abc123 --fork-session`.

**Por qué es útil:** permite explorar dos caminos distintos sin mezclarlos. Con `--continue` se sigue en la misma línea de siempre. Con `--fork-session` desde un punto específico, se crea una copia independiente que puede evolucionar por su cuenta, sin tocar la sesión original.

Es el mismo concepto que en Git: `--continue` es como seguir haciendo commits en la misma rama, mientras que `--fork-session` es como crear una rama nueva (`git switch -c`) desde un commit específico, para explorar algo distinto sin afectar `main`.

---

## Modelos

**Opus**: Razonamiento complejo. Research, Refactors, migraciones y features complejas.

**Sonnet**: Tareas de código de todos los días (componentes, bibliotecas, módulos, features pequeñas).

**Haiku**: Rápido y eficiente para tareas simples (scripts, utilerías).

Dependiendo de qué tan específico sea el pedido, es posible que se necesite un modelo más bajo.

---

## Configuración de Modos de Permiso

| Modo | Descripción resumida |
| --- | --- |
| `default` | Solicita permiso la primera vez que se usa cada herramienta. |
| `acceptEdits` | Auto-acepta edición de archivos y comandos comunes del sistema. |
| `plan` | Modo lectura: Claude analiza archivos pero no puede modificarlos. |
| `auto` | Auto-aprueba ejecuciones con revisiones de seguridad automáticas. |
| `dontAsk` | Deniega todo por defecto salvo reglas específicas pre-aprobadas. |
| `bypassPermissions` | Sin confirmaciones, excepto para comandos críticos o peligrosos. |

---

## Atajos y prefijos de la terminal

### Prefijos para escribir en el prompt

- `!` for shell mode
- `/` for commands
- `@` for file paths
- `&` for background
- `/btw` for side question

### Edición del texto que escribes

- Double tap `esc` to clear input
- `shift + tab` to auto-accept edits
- backslash (`\`) + return (`↵`) for newline

### Control de la ejecución y la salida

- `ctrl + o` for verbose output
- `ctrl + t` to toggle tasks
- `ctrl + s` to stash prompt
- `ctrl + g` to edit in `$EDITOR`

### Deshacer y pegar

- `ctrl + shift + _` to undo
- `ctrl + z` to suspend
- `ctrl + v` to paste images

### Cambiar configuración al vuelo

- `alt + p` to switch model
- `alt + o` to toggle fast mode

### Personalización

- `/keybindings` to customize

### En profundidad

- **Prefijos**: `!` ejecuta un comando de terminal directo (por ejemplo `git status`) sin pasar por el modelo; `/` activa un slash command como `/model` o `/loop`; `@` ayuda a referenciar un archivo específico del proyecto mientras se escribe; `&` manda algo a ejecutarse en segundo plano sin bloquear la conversación; `/btw` sirve para hacer una pregunta lateral sin interrumpir el flujo principal de la tarea en curso.
- **Edición**: doble `Esc` limpia el input; `Shift + Tab` equivale a saltar rápido al modo `acceptEdits`; `\` + `Enter` inserta un salto de línea en el mismo mensaje en vez de enviarlo.
- **Ejecución y salida**: `Ctrl + O` muestra salida detallada (verbose); `Ctrl + T` muestra u oculta la lista de tareas en curso; `Ctrl + S` guarda el prompt actual sin enviarlo; `Ctrl + G` abre el prompt en el editor configurado (`$EDITOR`) para escribir algo largo con más comodidad.
- **Deshacer y pegar**: `Ctrl + Shift + _` deshace la última acción; `Ctrl + Z` suspende la sesión (la manda a segundo plano en la terminal); `Ctrl + V` pega imágenes directamente en el chat.
- **Configuración al vuelo**: `Alt + P` cambia de modelo (Opus, Sonnet, Haiku) sin escribir `/model`; `Alt + O` activa o desactiva el fast mode.
- **Personalización**: `/keybindings` abre la configuración para personalizar estos atajos.

---

## Lo que aprendí

- Una sesión de Claude Code no vive "en general": vive ligada a la carpeta exacta desde la que se lanzó.
- La jerarquía de carpetas (padre → hija) determina qué contexto se hereda; las carpetas hermanas están aisladas entre sí salvo que se comparta explícitamente.
