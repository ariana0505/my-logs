# 06. git status

`git status` sirve para **consultar el estado del repositorio**. Muestra qué archivos tienen cambios, cuáles están preparados para el próximo commit y cuáles son nuevos y todavía no tienen seguimiento.

## 1. Consultar el estado

Dentro del repositorio, ejecuta:

```bash
git status
```

Puedes usarlo antes de preparar cambios, después de `git add` y después de crear un commit. Es un comando de consulta: no modifica archivos ni registra versiones.

## 2. Entender los mensajes principales

| Mensaje | Significado |
|---|---|
| `On branch main` | Estás trabajando en la rama `main`. El nombre puede ser distinto en otro proyecto. |
| `Untracked files` | Archivos nuevos que Git todavía no sigue y que no están ignorados. |
| `Changes not staged for commit` | Cambios en archivos con seguimiento que todavía no preparaste para el próximo commit. |
| `Changes to be committed` | Cambios preparados que incluiría un commit normal. |
| `nothing to commit, working tree clean` | No hay cambios pendientes detectados por este estado. |

Un directorio de trabajo limpio no demuestra por sí solo que todo esté publicado en GitHub. Puedes tener commits locales pendientes de enviar. Además, los archivos ignorados no aparecen de forma predeterminada.

## 3. Ejemplo de salida

```text
On branch main

Changes to be committed:
    modified: archivo1.md

Changes not staged for commit:
    modified: archivo2.md

Untracked files:
    archivo3.md
```

Esta salida indica:

1. Los cambios preparados de `archivo1.md` entrarían en el próximo commit normal.
2. Las modificaciones de `archivo2.md` todavía no están preparadas.
3. `archivo3.md` es un archivo nuevo sin seguimiento.

## 4. Un archivo puede aparecer en dos categorías

Si preparas un archivo con `git add` y después vuelves a editarlo, puede aparecer tanto en `Changes to be committed` como en `Changes not staged for commit`.

Esto significa que una versión de su contenido ya está preparada, pero hay modificaciones posteriores que todavía no lo están. Para incluir esas modificaciones, vuelve a ejecutar `git add` sobre el archivo.

## 5. Consultar una salida corta

```bash
git status --short
```

Ejemplos habituales:

```text
 M archivo1.md
M  archivo2.md
MM archivo3.md
?? archivo4.md
```

| Indicador | Significado en estos ejemplos |
|---|---|
| ` M` | El archivo tiene modificaciones sin preparar. |
| `M ` | El archivo tiene modificaciones preparadas. |
| `MM` | El archivo tiene modificaciones preparadas y modificaciones posteriores sin preparar. |
| `??` | El archivo no tiene seguimiento. |

Para archivos con seguimiento, la primera columna describe el estado preparado y la segunda describe el estado del directorio de trabajo respecto de lo preparado. Los espacios forman parte del indicador.

## 6. Ejemplo con tus apuntes

Desde `Logs`, después de modificar y guardar el archivo del punto 6:

```bash
git status
git add "git y github/06 - git status.md"
git status
```

La segunda consulta permite comprobar que preparaste el apunte correcto y revisar si ya había cambios de otros archivos preparados.

## Idea principal

**`git status` responde: «¿Qué cambió y qué está preparado para el próximo commit?».** Úsalo para comprobar el estado antes de registrar una versión.

## Documentación

- [Referencia oficial de git status](https://git-scm.com/docs/git-status)
