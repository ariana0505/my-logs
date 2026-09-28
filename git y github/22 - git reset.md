# 22. git reset

`git reset` permite **ajustar el área de preparación** y, cuando indicas un commit como destino sin limitar la operación a archivos, **cambiar la posición de tu rama actual**.

Su efecto depende de la forma del comando. En este punto usaremos el modo predeterminado, `--mixed`, que conserva el contenido del directorio de trabajo.

## 1. Quitar un archivo del área de preparación

Imagina que editaste y guardaste `apuntes.md`, y después ejecutaste:

```bash
git add apuntes.md
```

El contenido está preparado para el próximo commit. Si quieres quitarlo de esa selección:

```bash
git reset -- apuntes.md
```

El área de preparación de ese archivo vuelve a su estado del commit actual, pero **tu archivo conserva las ediciones**. Este uso no mueve la rama ni deshace un commit.

| Antes del reset | Después del reset |
|---|---|
| El archivo tiene cambios preparados. | Los cambios dejan de estar preparados. |
| Tu edición está en el archivo. | Tu edición permanece en el archivo. |

Si el archivo era nuevo y no existía en el commit actual, deja de estar preparado y vuelve a aparecer como archivo sin seguimiento.

El separador `--` indica que lo siguiente es una ruta.

## 2. Quitar todos los cambios preparados

```bash
git reset
```

Sin indicar otro commit ni una ruta, usa el commit actual como destino. Ajusta toda el área de preparación a ese commit y conserva tus archivos de trabajo.

**No retrocede la rama**, porque el destino es su posición actual. Puedes revisar el resultado con `git status`.

## 3. Retroceder un commit conservando los archivos

Supón que tu rama tiene este historial lineal:

```text
A → B → C   ← rama actual
```

Si ejecutas:

```bash
git reset HEAD~1
```

La rama vuelve a apuntar a `B`:

```text
A → B       ← rama actual
```

Git ajusta el área de preparación a `B`, pero **no cambia el contenido de tus archivos de trabajo**. Las diferencias respecto de `B` quedan pendientes y sin preparar; los archivos que no existían en `B` pueden quedar sin seguimiento.

Es como decir: «Retira el último commit de esta línea de trabajo, pero conserva el contenido para revisarlo o volver a registrarlo».

Si tenías ediciones pendientes además del contenido de `C`, también permanecen en los archivos. El comando no separa automáticamente esas ediciones del trabajo registrado en `C`.

## 4. Qué significa HEAD~1

`HEAD` identifica tu posición actual. Cuando trabajas normalmente en una rama, corresponde a su último commit.

`HEAD~1` indica el primer padre de ese commit: en un historial lineal, el commit anterior. En un commit de merge, sigue la línea del primer padre.

El ejemplo requiere que exista un commit padre. No puedes retroceder con `HEAD~1` desde el primer commit de un historial sin padres.

## 5. Por qué se conserva el contenido

En esta forma del comando, el modo predeterminado es `--mixed`:

```bash
git reset HEAD~1
```

Equivale a:

```bash
git reset --mixed HEAD~1
```

Actualiza la rama y el área de preparación, pero mantiene el directorio de trabajo.

| Modo con destino HEAD~1 | Rama | Área de preparación | Archivos de trabajo |
|---|---|---|---|
| `--soft` | Retrocede. | Se conserva. | Se conservan. |
| `--mixed` | Retrocede. | Se ajusta al destino. | Se conservan. |
| `--hard` | Retrocede. | Se ajusta al destino. | Se ajustan al destino. |

El punto 23 explica `--hard` por separado.

## 6. Ejemplo con tus apuntes: dejar de preparar un archivo

Después de editar y guardar el apunte, desde `Logs`:

```bash
git add "git y github/22 - git reset.md"
git status
git reset -- "git y github/22 - git reset.md"
git status
```

Puedes comprobar que la edición continúa en el archivo, pero ya no está preparada. La rama conserva sus commits.

## 7. Historial local y commits compartidos

Retroceder con reset hace que ciertos commits dejen de estar en la línea alcanzable desde la rama actual. No significa que Git borre inmediatamente esos objetos de todas partes: pueden seguir referenciados por otras ramas o conservarse temporalmente en registros locales.

La operación no modifica automáticamente el repositorio de GitHub.

Si un commit ya fue compartido y quieres deshacer sus cambios conservando el historial compartido, normalmente se utiliza `git revert`, que crea un nuevo commit inverso.

## Idea principal

**`git reset -- archivo` quita ese contenido de la preparación sin mover la rama. `git reset HEAD~1` retrocede la rama y conserva el contenido de los archivos como trabajo pendiente.**

## Documentación

- [Referencia oficial de git reset](https://git-scm.com/docs/git-reset)
- [Referencia oficial de git revert](https://git-scm.com/docs/git-revert)
