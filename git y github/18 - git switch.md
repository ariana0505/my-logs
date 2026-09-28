# 18. git switch

`git switch` es un comando dedicado a **cambiar de rama**. También permite crear una rama nueva y empezar a trabajar en ella.

## 1. Cambiar a una rama existente

Dentro del repositorio, si `mejorar-apuntes` ya existe:

```bash
git switch mejorar-apuntes
```

Git cambia la rama actual y actualiza los archivos según la versión de destino, conservando los cambios pendientes compatibles.

Para comprobar dónde estás:

```bash
git branch
```

El asterisco `*` aparece junto a la rama actual.

## 2. Regresar a main

Si la rama existe:

```bash
git switch main
```

Cambiar de rama no integra automáticamente los commits de la rama anterior en `main`.

## 3. Crear una rama y cambiar a ella

Si `mejorar-apuntes` todavía no existe:

```bash
git switch -c mejorar-apuntes
```

`-c` indica que quieres crear una rama. Sin especificar otro punto de partida, se crea desde tu posición actual y pasa a ser la rama de trabajo.

Si la rama ya existe, cambia a ella sin `-c`.

## 4. Diferencia con git checkout

**`git switch` se centra en el cambio de ramas; `git checkout` tiene varios usos**, entre ellos cambiar de rama y restaurar archivos.

Para estos casos habituales, los comandos son equivalentes:

| Acción | Con git switch | Con git checkout |
|---|---|---|
| Cambiar a una rama existente | `git switch main` | `git checkout main` |
| Crear una rama y cambiar a ella | `git switch -c nueva-rama` | `git checkout -b nueva-rama` |

`checkout` también puede restaurar un archivo con:

```bash
git checkout -- archivo.md
```

En este uso, reemplaza el contenido del archivo por su versión del área de preparación y descarta las modificaciones sin preparar de ese archivo. No es una operación de cambio de rama y `git switch` no realiza esa acción.

Para tus prácticas, usa `git switch` cuando quieras cambiar de rama: expresa claramente esa intención. `git checkout` sigue siendo válido y aparece en muchos tutoriales.

## 5. Qué pasa con los cambios pendientes

Cambiar de rama no guarda automáticamente tus ediciones en el historial:

- Si los cambios locales son compatibles, pueden acompañarte a la otra rama.
- Si la operación sobrescribiría cambios locales de forma incompatible, Git normalmente bloquea el cambio.

Consulta el estado antes de cambiar:

```bash
git status
```

Si quieres conservar una versión en el historial, prepara los cambios y crea un commit. Si quieres guardarlos temporalmente sin registrar una versión en la rama, puedes usar `git stash`, explicado en el punto 19.

## 6. Ejemplo con tus apuntes

Este ejemplo supone que estás en `main` y que `mejorar-apuntes` todavía no existe:

```bash
cd /Users/ariana/Desktop/Logs
git status
git switch -c mejorar-apuntes
git branch
```

Ahora los commits que crees normalmente harán avanzar `mejorar-apuntes`.

Cuando hayas conservado tu trabajo y quieras regresar:

```bash
git status
git switch main
```

## Idea principal

**`git switch nombre` cambia a una rama existente; `git switch -c nombre` crea una rama y cambia a ella.** Consulta el estado antes para entender qué trabajo sigue pendiente.

## Documentación

- [Referencia oficial de git switch](https://git-scm.com/docs/git-switch)
- [Referencia oficial de git checkout](https://git-scm.com/docs/git-checkout)
