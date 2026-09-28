# 16. git push y git pull

`git push` y `git pull` permiten intercambiar trabajo con un repositorio remoto. **Push publica commits; pull obtiene cambios remotos y los integra en tu rama actual.**

## 1. git push: publicar tus commits

Si tienes una rama local llamada `main` y un remoto llamado `origin`:

```bash
git push origin main
```

El comando envía los datos necesarios para actualizar la rama `main` del remoto a partir de tu rama local `main`, si el servidor acepta la operación.

| Parte | Significado |
|---|---|
| `git push` | Publica commits y actualiza referencias remotas. |
| `origin` | Remoto al que quieres enviar el trabajo. |
| `main` | Rama local que quieres publicar en la rama remota del mismo nombre. |

**Push no publica directamente las ediciones pendientes ni el contenido que solo preparaste con `git add`.** Primero debes crear un commit. Puedes enviar varios commits pendientes con un solo push.

## 2. Establecer el seguimiento de una rama

Para publicar una rama y establecer su relación de seguimiento:

```bash
git push -u origin main
```

`-u` corresponde a `--set-upstream`. Cuando la publicación se realiza correctamente o la rama ya está actualizada, configura el seguimiento hacia la rama remota correspondiente.

Con esa relación configurada y una configuración habitual de Git, puedes usar:

```bash
git push
```

En tu proyecto `Logs`, la rama `main` ya tiene seguimiento configurado.

## 3. git pull: obtener e integrar cambios

```bash
git pull origin main
```

Este comando hace dos cosas:

1. Obtiene información y commits de la rama remota mediante una operación de fetch.
2. Intenta integrar la rama indicada en **la rama en la que estás trabajando**.

Especificar `main` como origen no cambia automáticamente tu rama actual a `main`. Para actualizar tu rama local `main` con ese comando, comprueba primero que estás trabajando en ella.

Con una relación de seguimiento configurada, normalmente puedes usar:

```bash
git pull
```

Git utiliza el seguimiento para identificar la rama remota que debe integrar.

## 4. Cómo se integran los cambios

El resultado depende de las opciones y la configuración:

- **Avance directo o fast-forward:** la rama local avanza cuando no hay una divergencia que requiera otra forma de integración.
- **Merge:** combina los historiales; cuando hace falta, crea un commit de integración.
- **Rebase:** vuelve a aplicar tus commits locales sobre la historia obtenida del remoto.

Por ejemplo, esta opción permite únicamente un avance directo y se detiene si las ramas han divergido:

```bash
git pull --ff-only
```

Si hay divergencia, debes revisar el historial y elegir la forma de integración adecuada al proyecto. No asumas que cualquier pull tendrá el mismo resultado.

Durante un merge o un rebase pueden aparecer conflictos si Git no puede combinar automáticamente los cambios. Tendrás que resolverlos para completar esa integración.

## 5. Revisar antes de actualizar

Antes de obtener e integrar cambios, consulta:

```bash
git status
git branch
```

Comprueba la rama actual y si hay trabajo pendiente. Los cambios sin registrar pueden impedir una integración si esta necesita modificar los mismos archivos. Conserva tu trabajo antes de continuar.

Si el remoto está en GitHub, necesitas conexión para intercambiar datos y permisos para publicar.

## 6. Ejemplo con dos computadoras

Imagina que registras un cambio en la computadora A y lo publicas:

```text
Computadora A → commit → push → GitHub
```

Después, desde la computadora B, obtienes e integras ese trabajo:

```text
GitHub → pull → computadora B
```

Ambas computadoras tienen repositorios locales. GitHub sirve como ubicación compartida para intercambiar sus commits.

## 7. Ejemplo de publicación con tus apuntes

Después de editar y guardar un apunte, desde `Logs`:

```bash
git status
git add "git y github/16 - git push y git pull.md"
git diff --staged
git commit -m "docs: explain push and pull"
git push
```

Revisa todos los cambios preparados antes del commit. El commit normal incluye también cualquier otro cambio que ya estuviera preparado.

Si el remoto tiene commits que tu rama no integra, el push puede ser rechazado. Debes consultar e integrar el historial remoto antes de volver a publicar.

## Resumen

| Comando | Resultado |
|---|---|
| `git push origin main` | Publica la rama local `main` en `main` del remoto `origin`. |
| `git push -u origin main` | Publica y establece el seguimiento de la rama. |
| `git push` | Publica según el seguimiento y la configuración aplicables. |
| `git pull origin main` | Obtiene `main` del remoto y la integra en tu rama actual. |
| `git pull` | Obtiene e integra la rama de seguimiento configurada. |

## Idea principal

**Push comparte tus commits con el remoto. Pull obtiene trabajo del remoto y lo integra en tu rama actual.** Crear un commit, publicarlo y obtener cambios de otras personas son acciones distintas.

## Documentación

- [Referencia oficial de git push](https://git-scm.com/docs/git-push)
- [Referencia oficial de git pull](https://git-scm.com/docs/git-pull)
