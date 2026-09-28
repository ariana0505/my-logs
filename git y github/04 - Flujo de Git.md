# 04. Flujo de Git

El flujo básico de Git consiste en **editar archivos, preparar los cambios y registrarlos en un commit**. Después puedes compartir los commits con un repositorio remoto, por ejemplo uno alojado en GitHub.

## 1. Las tres zonas de Git

| Zona | Qué contiene | Ejemplo |
|---|---|---|
| **Directorio de trabajo** (*working tree*) | Los archivos del proyecto que puedes consultar y editar. | Modificas un apunte y guardas el archivo. |
| **Área de preparación** (*staging area* o *index*) | El contenido seleccionado para el próximo commit. | Preparas ese apunte con `git add`. |
| **Repositorio local** | El historial de commits almacenado en tu computadora. | Registras la explicación con `git commit`. |

Los comandos conectan esas zonas:

```text
Archivos editados
       │
       │ git add
       ▼
Cambios preparados
       │
       │ git commit
       ▼
Historial local
       │
       │ git push
       ▼
Repositorio remoto, por ejemplo en GitHub
```

El repositorio remoto es otro repositorio con el que intercambias commits; no es una de las tres zonas locales.

## 2. Editar y guardar un archivo

Imagina que agregas una explicación a este apunte:

```text
git y github/02 - git config.md
```

Al guardar el archivo en tu editor, la modificación queda en el directorio de trabajo. **Guardar un archivo no crea un commit.**

## 3. Revisar el estado con git status

Desde la carpeta `Logs`, ejecuta:

```bash
git status
```

Este comando permite distinguir:

- **Archivos nuevos sin seguimiento** (*untracked*): todavía no están incorporados al seguimiento de Git.
- **Cambios sin preparar**: modificaciones que aún no seleccionaste para el próximo commit.
- **Cambios preparados**: contenido que se incluirá si haces un commit normal.

Puedes ejecutar `git status` antes y después de preparar los cambios. Consultar el estado no modifica los archivos ni crea commits.

## 4. Preparar los cambios con git add

Desde `Logs`, prepara el apunte con:

```bash
git add "git y github/02 - git config.md"
```

El comando actualiza el área de preparación con el contenido actual de ese archivo. Puedes preparar archivos nuevos y modificaciones de archivos que Git ya sigue.

**`git add` no crea un commit ni envía archivos a GitHub.**

### ¿Qué pasa si vuelves a editar el archivo?

Supón que haces lo siguiente:

1. Agregas una explicación y guardas el archivo.
2. Ejecutas `git add`.
3. Agregas otro párrafo y vuelves a guardar.

El área de preparación conserva el contenido del paso 2. Para incluir también el nuevo párrafo, debes ejecutar `git add` otra vez.

Un archivo puede tener al mismo tiempo cambios preparados y cambios sin preparar.

## 5. Crear un commit

```bash
git commit -m "docs: explain Git configuration"
```

Un commit normal registra el estado preparado y lo incorpora al historial local.

| Parte | Función |
|---|---|
| `git commit` | Crea un commit con el contenido preparado. |
| `-m` | Permite indicar el mensaje directamente en el comando. |
| `"docs: explain Git configuration"` | Describe el cambio realizado. |

En este ejemplo, `docs:` es una convención para señalar un cambio de documentación. No es una palabra obligatoria de Git.

Si preparaste cambios de varios archivos, el mismo commit puede incluirlos. Los cambios sin preparar quedan pendientes en tu directorio de trabajo.

**Crear un commit no sube los cambios a GitHub.** El commit se guarda en tu computadora y puedes crearlo sin conexión a internet.

## 6. Compartir los commits con git push

En tu repositorio, que ya tiene un remoto y una rama de seguimiento configurados, puedes ejecutar:

```bash
git push
```

También puedes indicar explícitamente el remoto y la rama:

```bash
git push origin main
```

| Parte | Significado |
|---|---|
| `git push` | Envía los datos necesarios para actualizar referencias en el repositorio remoto. |
| `origin` | Es el nombre del remoto al que quieres enviar los commits. |
| `main` | Es la rama local que quieres publicar en la rama del mismo nombre en el remoto. |

`origin` es un nombre habitual para un remoto y `main` es un nombre habitual para una rama; otros proyectos pueden usar nombres distintos.

**`git push` comparte commits; no publica directamente los cambios que solo hayas editado o preparado.** Puede enviar varios commits locales pendientes en una sola operación.

Si el remoto está alojado en internet, necesitas conexión y autorización para escribir en él. En un repositorio nuevo, primero debes configurar el remoto y la relación de seguimiento para usar este flujo con `git push` sin argumentos.

## 7. Ejemplo completo con tus apuntes

Primero edita y guarda `02 - git config.md`. Después, ejecuta estas líneas una por una:

```bash
cd /Users/ariana/Desktop/Logs
git status
git add "git y github/02 - git config.md"
git status
git commit -m "docs: explain Git configuration"
git push
git status
```

La secuencia permite:

1. Entrar en el proyecto.
2. Consultar los cambios pendientes.
3. Preparar el apunte elegido.
4. Comprobar qué está preparado antes de crear el commit.
5. Registrar los cambios preparados en el historial local.
6. Compartir los commits con el remoto.
7. Revisar el estado final.

Si ya habías preparado cambios de otros archivos, revisa el segundo `git status`: un commit normal también incluirá esos cambios preparados.

Si no hay cambios preparados respecto del último commit, este `git commit` no creará uno nuevo. Después del commit, pueden seguir apareciendo modificaciones de otros archivos que no hayas incluido.

## 8. Relación con el trabajo en equipo

Este ejemplo muestra cómo publicar tu trabajo. En un proyecto compartido también necesitas consultar e integrar los cambios de otras personas. Más adelante veremos `git fetch` y `git pull`.

Si el remoto tiene cambios que tu rama aún no integra, el push puede ser rechazado. En ese caso hay que revisar e integrar el historial remoto antes de volver a publicar.

## Idea principal

| Acción | Resultado |
|---|---|
| Guardar en el editor | Conserva la edición del archivo en tu computadora. |
| `git add` | Prepara el contenido para el próximo commit. |
| `git commit` | Registra una versión en el historial local. |
| `git push` | Comparte los commits con el repositorio remoto. |

**Editar → preparar → registrar → compartir** es el flujo que repetirás al trabajar con Git y un remoto.

## Documentación

- [Manual de Git](https://git-scm.com/docs/user-manual)
- [git status](https://git-scm.com/docs/git-status)
- [git add](https://git-scm.com/docs/git-add)
- [git commit](https://git-scm.com/docs/git-commit)
- [git push](https://git-scm.com/docs/git-push)
