# 12. git branch

`git branch` permite **consultar y administrar las ramas del repositorio**. En este punto aprenderás a listar las ramas locales y crear una nueva sin cambiar tu ubicación de trabajo.

## 1. Consultar las ramas locales

Dentro del repositorio, ejecuta:

```bash
git branch
```

Ejemplo de salida:

```text
* main
  mejorar-apuntes
```

El asterisco `*` indica la rama actual. En este ejemplo estás trabajando en `main`; `mejorar-apuntes` también existe, pero no es la rama actual.

Consultar la lista no cambia de rama ni modifica tus archivos.

## 2. Crear una rama

Si estás en `main` y la rama nueva todavía no existe:

```bash
git branch mejorar-apuntes
```

Crea `mejorar-apuntes` desde tu posición actual. Inicialmente apunta al mismo commit desde el que la creaste.

**Este comando crea la rama, pero no cambia a ella.** Si estabas en `main`, sigues en `main`.

Puedes comprobarlo con:

```bash
git branch
```

La salida mostrará:

```text
* main
  mejorar-apuntes
```

Crear la rama no registra automáticamente las ediciones pendientes en tus archivos. La rama es una referencia a un commit, no una copia de los cambios sin registrar.

## 3. Empezar a trabajar en la nueva rama

Para cambiar a una rama que ya creaste, puedes usar:

```bash
git checkout mejorar-apuntes
```

Ese comando se explica en el punto 13. Después del cambio, `git branch` mostrará el asterisco junto a `mejorar-apuntes`.

## 4. Consultar referencias de seguimiento remoto

```bash
git branch -r
```

Muestra las referencias de seguimiento remoto almacenadas en tu repositorio local, por ejemplo `origin/main`.

Estas referencias representan la información que tu repositorio tiene de las ramas remotas. El comando no consulta GitHub en tiempo real; esa información se actualiza mediante operaciones como `git fetch`.

## 5. Ejemplo con tus apuntes

Este ejemplo supone que ya estás en `main` y que `mejorar-apuntes` todavía no existe:

```bash
cd /Users/ariana/Desktop/Logs
git status
git branch
git branch mejorar-apuntes
git branch
```

La secuencia permite revisar el estado del proyecto, comprobar la rama actual, crear la nueva rama y verificar que existe.

Después de estos comandos sigues en `main`. Para hacer avanzar la rama nueva con tus próximos commits, primero debes cambiar a ella.

## Resumen de comandos

| Comando | Resultado |
|---|---|
| `git branch` | Lista las ramas locales y marca la actual con `*`. |
| `git branch nombre` | Crea una rama desde la posición actual sin cambiar a ella. |
| `git branch -r` | Lista las referencias de seguimiento remoto conocidas localmente. |

## Idea principal

**Crear una rama y cambiar a ella son acciones distintas. `git branch nombre` crea la rama; no te coloca en ella.**

## Documentación

- [Referencia oficial de git branch](https://git-scm.com/docs/git-branch)
- [Manual de Git](https://git-scm.com/docs/user-manual)
