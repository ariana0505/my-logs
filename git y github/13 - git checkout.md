# 13. git checkout

`git checkout` permite, entre otros usos, **cambiar de rama**. En este punto nos centraremos en cambiar a una rama existente y en crear una rama nueva mientras empiezas a trabajar en ella.

## 1. Cambiar a una rama existente

Si la rama `mejorar-apuntes` ya existe, ejecuta dentro del repositorio:

```bash
git checkout mejorar-apuntes
```

Git cambia la rama actual y actualiza los archivos del directorio de trabajo según la versión de destino, conservando los cambios pendientes compatibles.

Para comprobar la rama actual:

```bash
git branch
```

Ejemplo de salida:

```text
  main
* mejorar-apuntes
```

El asterisco confirma que estás trabajando en `mejorar-apuntes`.

## 2. Regresar a la rama principal

Si tu rama principal se llama `main`:

```bash
git checkout main
```

Cambiar de rama no fusiona sus historiales. Los commits que registraste en `mejorar-apuntes` permanecen en esa línea de trabajo hasta que decidas integrarlos en otra rama.

El nombre de la rama principal puede ser distinto en otros proyectos.

## 3. Crear una rama y cambiar a ella

Si la rama todavía no existe:

```bash
git checkout -b mejorar-apuntes
```

La opción `-b` indica que quieres crear una rama nueva y cambiar a ella. Sin especificar otro punto de partida, se crea desde tu posición actual.

En el caso habitual, equivale a estas dos acciones:

```bash
git branch mejorar-apuntes
git checkout mejorar-apuntes
```

Si ya creaste la rama, usa `git checkout mejorar-apuntes` sin `-b`. Intentar crear otra rama con el mismo nombre produce un error.

## 4. ¿Qué pasa con los cambios sin commit?

**Cambiar de rama no registra tus cambios pendientes ni los asigna automáticamente al historial de una rama.**

- Si son compatibles con el cambio de rama, Git puede conservarlos y aparecerán pendientes en la nueva ubicación de trabajo.
- Si cambiar de rama sobrescribiría cambios locales de forma incompatible, Git normalmente bloquea la operación y muestra un mensaje.

Por eso conviene revisar el estado antes de cambiar:

```bash
git status
```

Si quieres conservar una versión en el historial de la rama actual, prepara los cambios y crea un commit antes de cambiar. Más adelante veremos `git stash` para guardar temporalmente trabajo pendiente.

## 5. Ejemplo con tus apuntes

Este ejemplo supone que estás en `main`, que `mejorar-apuntes` todavía no existe y que no hay cambios pendientes que interfieran:

```bash
cd /Users/ariana/Desktop/Logs
git status
git checkout -b mejorar-apuntes
git branch
```

Ahora estás en la rama nueva. Si editas un apunte, lo preparas con `git add` y creas un commit, normalmente ese commit hará avanzar `mejorar-apuntes`.

Cuando quieras regresar, consulta primero el estado y luego cambia:

```bash
git status
git checkout main
```

## 6. Relación con git switch

`git checkout` tiene varios usos además del cambio de ramas. Git también ofrece `git switch`, un comando dedicado a trabajar con ramas, que veremos en el punto 18.

Para estos ejemplos:

| Con git checkout | Con git switch | Resultado |
|---|---|---|
| `git checkout mejorar-apuntes` | `git switch mejorar-apuntes` | Cambia a una rama existente. |
| `git checkout -b mejorar-apuntes` | `git switch -c mejorar-apuntes` | Crea una rama y cambia a ella. |

## Resumen de comandos

| Comando | Resultado |
|---|---|
| `git checkout nombre` | Cambia a una rama existente. |
| `git checkout main` | Cambia a `main`, si esa rama existe. |
| `git checkout -b nombre` | Crea una rama nueva y cambia a ella. |
| `git branch` | Permite comprobar qué rama está activa. |

## Idea principal

**`git checkout nombre` cambia a una rama existente. `git checkout -b nombre` crea una rama nueva y cambia a ella.** Antes de hacerlo, consulta `git status` para entender qué trabajo sigue pendiente.

## Documentación

- [Referencia oficial de git checkout](https://git-scm.com/docs/git-checkout)
- [Referencia oficial de git switch](https://git-scm.com/docs/git-switch)
