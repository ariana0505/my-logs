# 07. git commit

`git commit` sirve para **registrar una versión del proyecto en el historial local**. En su uso normal, registra el estado del área de preparación junto con un mensaje que describe el cambio.

## 1. ¿Qué es un commit?

Un commit es un registro de una versión del proyecto. Incluye el estado registrado de los archivos con seguimiento, información de autoría, un mensaje y referencias a sus commits anteriores cuando los tiene.

Cada commit tiene un identificador que permite distinguirlo y consultarlo en el historial.

## 2. Preparar los cambios antes de registrarlos

Después de editar y guardar un archivo, prepáralo con `git add`. Desde `Logs`:

```bash
git add "git y github/07 - git commit.md"
git status
```

Comprueba en `Changes to be committed` qué contenido estás a punto de registrar.

## 3. Crear un commit con un mensaje

```bash
git commit -m "docs: explain git commit"
```

| Parte | Función |
|---|---|
| `git commit` | Crea un commit con el estado preparado. |
| `-m` | Permite escribir el mensaje directamente en el comando. |
| `"docs: explain git commit"` | Describe el cambio registrado. |

`docs:` es una convención para señalar cambios de documentación. Git no exige ese prefijo ni un idioma específico. En estos apuntes usamos mensajes en inglés.

## 4. ¿Qué cambios incluye?

Un commit normal incluye **todos los cambios preparados**, aunque hayas ejecutado `git add` varias veces sobre archivos diferentes.

Por ejemplo:

```bash
git add archivo1.md
git add archivo2.md
git commit -m "docs: update two notes"
```

El commit incluye el contenido preparado de ambos archivos. Los cambios sin preparar quedan pendientes en tu directorio de trabajo.

Si preparaste un archivo y lo editaste después, el commit registra la versión preparada. Las modificaciones posteriores solo se incluyen si vuelves a prepararlas.

## 5. Escribir un mensaje útil

El mensaje debe explicar el cambio de forma concreta. Ejemplos:

```text
docs: explain Git configuration
docs: add terminal navigation examples
docs: clarify the Git workflow
```

Mensajes como `changes` o `update` aportan poca información cuando consultas el historial.

Agrupa en cada commit cambios que tengan una relación clara, por ejemplo, la explicación y los ejemplos de un mismo tema.

## 6. ¿Qué pasa si no hay cambios preparados?

Si el área de preparación no contiene diferencias respecto del último commit, un `git commit -m` normal no crea un nuevo commit.

Puede mostrar que hay cambios sin preparar o que no hay nada que registrar. Usa `git status` para entender el estado.

## 7. Commit y push son acciones distintas

| Comando | Resultado |
|---|---|
| `git commit` | Registra una versión en tu repositorio local. |
| `git push` | Comparte commits con un repositorio remoto. |

Puedes crear commits sin conexión a internet. Si el remoto está en GitHub, necesitas conexión y autorización para publicar allí.

Un commit no sube automáticamente los archivos a GitHub. Puedes crear varios commits locales y enviarlos después con un solo push.

## 8. Ejemplo completo con tus apuntes

Después de editar y guardar el archivo del punto 7, ejecuta desde `Logs`:

```bash
git status
git add "git y github/07 - git commit.md"
git status
git commit -m "docs: explain git commit"
git status
```

La secuencia permite revisar los cambios, preparar el archivo, comprobar lo preparado, registrar la versión y consultar qué quedó pendiente.

Si había cambios de otros archivos preparados, también se incluirán en este commit normal. Por eso es útil revisar el estado justo antes de registrarlo.

## Idea principal

**`git commit` registra una versión con los cambios preparados. Ese registro queda en tu computadora hasta que lo compartes con un remoto.**

## Documentación

- [Referencia oficial de git commit](https://git-scm.com/docs/git-commit)
- [Tutorial de Git: área de preparación](https://git-scm.com/docs/gittutorial-2)
