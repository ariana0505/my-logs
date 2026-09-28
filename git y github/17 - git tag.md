# 17. git tag

Un **tag**, o **etiqueta**, es un nombre que marca un punto del historial, normalmente un commit importante. `git tag` permite crear y consultar estas etiquetas.

Puedes usarlas para identificar una versión terminada del proyecto, como `v1.0`, o una entrega de tus apuntes, como `apuntes-v1`.

## 1. Diferencia entre una rama y una etiqueta

```text
A ── B ── C ── D      main
          ↑
         v1.0
```

Cada letra representa un commit. En este ejemplo, `main` apunta a `D` y `v1.0` marca la versión registrada en `C`.

| Rama | Etiqueta |
|---|---|
| Representa una línea de trabajo. | Identifica un punto concreto del historial. |
| Avanza cuando creas commits normalmente sobre ella. | No avanza al crear nuevos commits. |
| Se usa para desarrollar cambios. | Se usa para marcar versiones o entregas. |

Una etiqueta puede modificarse explícitamente, pero no se mueve automáticamente con tus nuevos commits. Habitualmente se conserva para identificar la misma versión.

## 2. Crear una etiqueta sencilla

Dentro del repositorio:

```bash
git tag v1.0
```

Crea una etiqueta ligera llamada `v1.0` sobre el commit actual. Es una referencia directa, sin un objeto de anotación con mensaje y datos del creador.

**No registra las ediciones pendientes ni los cambios que solo preparaste con `git add`.** Si quieres que esos cambios formen parte de la versión etiquetada, primero debes crear un commit.

## 3. Crear una etiqueta anotada

```bash
git tag -a v1.0 -m "Release version 1.0"
```

Crea una etiqueta anotada sobre el commit actual. Incluye un mensaje, información de quién creó la etiqueta y la fecha.

| Parte | Función |
|---|---|
| `git tag` | Gestiona las etiquetas. |
| `-a` | Indica que quieres crear una etiqueta anotada. |
| `v1.0` | Es el nombre elegido. |
| `-m "Release version 1.0"` | Define el mensaje de la etiqueta. |

Los ejemplos de etiqueta ligera y anotada son alternativas. Si ya creaste `v1.0`, intentar crear otra con ese mismo nombre sin reemplazarla explícitamente producirá un error.

El nombre es una elección del proyecto: Git no exige que sea `v1.0` ni interpreta por sí solo qué significa esa versión.

## 4. Consultar las etiquetas

```bash
git tag
```

Ejemplo de salida:

```text
v1.0
v1.1
v2.0
```

Este comando consulta las etiquetas disponibles localmente. No las crea ni las publica.

## 5. Consultar una versión etiquetada

```bash
git show v1.0
```

Permite consultar la etiqueta y el commit que señala. En una etiqueta anotada, muestra también su anotación; la salida puede incluir información del commit y sus cambios.

Si se abre el visor habitual de la terminal, presiona `q` para salir.

## 6. Publicar una etiqueta en GitHub

Crear la etiqueta la guarda en tu repositorio local. Para publicarla en el remoto `origin`:

```bash
git push origin tag v1.0
```

Publica específicamente `v1.0` y envía los datos necesarios para que el remoto pueda referenciarla. No hace avanzar por sí solo una rama remota llamada `main`.

Un push normal de una rama no publica automáticamente todas tus etiquetas. Git tiene opciones y configuraciones para enviar etiquetas junto con ramas; el comando anterior permite indicar exactamente cuál quieres publicar.

## 7. Ejemplo con tus apuntes

Cuando hayas registrado en commits una primera versión completa de tus apuntes, y la etiqueta `apuntes-v1` todavía no exista:

```bash
cd /Users/ariana/Desktop/Logs
git status
git log --oneline -5
git tag -a apuntes-v1 -m "First complete version of Git notes"
git show apuntes-v1
git push origin tag apuntes-v1
```

La secuencia permite revisar el estado y los commits recientes, marcar el commit actual, consultar la versión etiquetada y publicar la etiqueta.

La etiqueta señala un commit del repositorio completo. No etiqueta solo la carpeta `git y github`, aunque su nombre describa esa entrega.

Crear etiquetas no exige que el directorio de trabajo esté limpio, pero comprobar el estado evita confundir las ediciones pendientes con la versión registrada que estás marcando.

## Idea principal

**Una rama sigue una línea de trabajo; un tag marca una versión concreta.** Crear una etiqueta y publicarla en un remoto son acciones distintas.

## Documentación

- [Referencia oficial de git tag](https://git-scm.com/docs/git-tag)
- [Modelo de datos de Git](https://git-scm.com/docs/gitdatamodel)
- [Referencia oficial de git push](https://git-scm.com/docs/git-push)
