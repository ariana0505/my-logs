Fecha : 25/09/26

# Scope en herramientas

---

## Objetivos de la clase 🎯

---

## Scope

Entender el sistema de scope que usa Claude Code nos ayuda a entender las configuraciones que se aplican al iniciar una sesión.

Scopes en Claude Code:

- Managed
- User
- Project
- Local

---

## Comparativa de Scopes

| Scope | Ubicación | Impacto | ¿Compartido? |
| --- | --- | --- | --- |
| Managed | `managed-settings.json` | Todos los usuarios | Sí (vía IT) |
| User | `~/.claude/settings.json` | Tú (globalmente) | No |
| Project | `.claude/settings.json` | Todos los colaboradores | Sí (git) |
| Local | `.claude/settings.local.json` | Solo tú (este repo) | No (gitignore) |

---

## Project

Es el mejor lugar para configuraciones compartidas con tu equipo.

Todo lo que se use para tu stack de desarrollo debería ir aquí:

- Plugins
- MCPs
- Permisos
- Hooks

Con esto estandarizamos las herramientas del equipo.

---

## Prioridad en configuraciones

Orden de prioridad del scope de las configuraciones:

1. Managed
2. Argumentos de la línea de comandos
3. Local
4. Project
5. User

---

## 💡 Dato curioso: `~/.claude/settings.json` vs `~/.claude.json`

A nivel User, en la práctica existen dos archivos distintos que cumplen roles diferentes:

- **`~/.claude/settings.json`**: es el archivo «limpio» que corresponde exactamente al scope User de la tabla de comparativa. Es pequeño y solo contiene preferencias de uso: modelo por defecto, nivel de esfuerzo, tema visual, notificaciones, etc. Está pensado para editarse a mano.
- **`~/.claude.json`**: es un archivo mucho más grande, de estado interno de la aplicación, no solo configuración. Ahí viven los servidores MCP conectados (por ejemplo Context7), el historial de proyectos abiertos, datos de la cuenta (`oauthAccount`, `userID`), caches de funcionalidades, contadores de uso, notificaciones ya vistas, etc. No está pensado para editarse directamente; es más bien el «cerebro» de datos que la app acumula al usarse.

Ambos viven en el mismo nivel (User), pero uno es configuración pensada para el usuario y el otro es estado interno de la aplicación.

---

## Scope por features

| Feature | User | Project | Local |
| --- | --- | --- | --- |
| Settings | `~/.claude/settings.json` | `.claude/settings.json` | `.claude/settings.local.json` |
| Subagents | `~/.claude/agents/` | `.claude/agents/` | None |
| MCP Servers | `~/.claude.json` | `.mcp.json` | `~/.claude.json` (per-project) |
| Plugins | `~/.claude/settings.json` | `.claude/settings.json` | `.claude/settings.local.json` |
| CLAUDE.md | `~/.claude/CLAUDE.md` | `CLAUDE.md` o `.claude/CLAUDE.md` | `CLAUDE.local.md` |

---

## Ubicación automática vs. manual al instalar

Depende de qué se esté instalando, pero en general Claude Code lo ubica automáticamente; solo se elige el scope al momento de instalarlo, sin mover archivos a mano después.

- **MCP servers**: con `claude mcp add` se puede indicar el scope con una bandera (`-s user`, `-s project`, `-s local`). Según lo elegido, Claude Code escribe la entrada en el archivo correcto de la tabla anterior (`~/.claude.json` para User, `.mcp.json` para Project).
- **Plugins**: se instalan con un comando y Claude Code decide en qué `settings.json` escribir la referencia según el scope pedido.
- **`CLAUDE.md`**: se crea y escribe a mano, en la carpeta correspondiente. No se genera automáticamente.
- **Subagents**: se guardan como archivos dentro de una carpeta `agents/`, normalmente creados o editados directamente ahí, aunque instalar un subagente empaquetado sí podría colocarlo automáticamente.

---

## Recomendaciones de configuración de permisos

### Modo del día a día

- `default` o `acceptEdits` para trabajo normal de aprendizaje y desarrollo.
  - `default`: pide permiso la primera vez que se usa cada herramienta, útil mientras se sigue aprendiendo qué hace cada una.
  - `acceptEdits`: auto-acepta ediciones de archivos y comandos comunes, pero sigue preguntando por lo raro o peligroso.
- Evitar `bypassPermissions` en proyectos con datos reales (por ejemplo, el registro de pagos por Yape), porque casi no pregunta nada y no da oportunidad de frenar un error a tiempo.

### Qué debería estar siempre bloqueado (deny)

- `rm -rf` sobre carpetas del proyecto o del sistema.
- `git push --force` / `git push -f`, sobre todo hacia `main`.
- `git reset --hard` sin haber revisado antes qué se perdería.
- `curl | bash` o `irm | iex` que descargue y ejecute un script de internet a ciegas.
- `sudo` en general, salvo saber exactamente qué comando es.
- Acceso o borrado de archivos con datos sensibles: `.env`, credenciales, o el archivo con los pagos reales de clientes.

### Qué está bien dejar en automático (allow)

- `git status`, `git diff`, `git log`.
- `cat`, `ls`, `find`, `grep` dentro del proyecto.
- Correr tests (`npm test`, `pytest`, etc.) y linters.

### Dónde se configura

En el `settings.json` del scope que corresponda, con listas de `allow` y `deny` para reglas específicas. Para un proyecto individual como el registro de pagos, iría en scope Project o Local; para reglas compartidas en equipo, en scope Project.

### Conexión con hooks

Un hook `PreToolUse` puede aplicar una de estas reglas de forma más robusta que un simple `deny` estático, por ejemplo bloqueando `git push --force` hacia `main` con lógica que verifique la rama actual antes de decidir.

---

## Links

- Claude Code Settings: [https://code.claude.com/docs/en/settings](https://code.claude.com/docs/en/settings)
