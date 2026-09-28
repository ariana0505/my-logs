# 11. ¿Qué es un Branch?

Un **branch**, o **rama**, es una línea de desarrollo dentro de un repositorio. Permite registrar una serie de cambios y mantenerla separada de otras líneas de trabajo hasta que decidas integrarlas.

Las ramas pueden compartir parte del historial. Crear una rama no significa crear una carpeta nueva ni duplicar todo el proyecto.

## 1. ¿Para qué sirve una rama?

Puedes usar una rama para:

- Probar una idea o una nueva organización del proyecto.
- Desarrollar una función.
- Corregir un error.
- Preparar cambios que todavía no quieres integrar en la rama principal.

Cuando el trabajo esté listo, puedes integrar sus cambios en otra rama mediante un *merge*. Más adelante veremos el comando correspondiente.

## 2. Ejemplo con tus apuntes

Imagina que tus apuntes están en una rama llamada `main` y quieres probar una nueva organización. Creas otra rama llamada `reorganizar-apuntes` a partir del commit actual y registras allí tus cambios:

```text
A ── B ── C             main
          \
           D ── E       reorganizar-apuntes
```

Cada letra representa un commit:

| Elemento | Significado |
|---|---|
| `A`, `B` y `C` | Son el historial compartido por ambas ramas. |
| `D` y `E` | Registran los cambios hechos en `reorganizar-apuntes`. |
| `main` | Sigue apuntando al commit `C`. |
| `reorganizar-apuntes` | Apunta al commit `E`. |

Los commits `D` y `E` no pasan a formar parte del historial de `main` solo por existir. Para incorporarlos, debes realizar una operación de integración.

## 3. ¿Qué es una rama técnicamente?

Una rama es una **referencia con nombre a un commit**. Ese commit representa la punta de su línea de desarrollo. Git recorre los commits anteriores para conocer el historial alcanzable desde esa referencia.

Puedes imaginarla como un marcador que señala hasta dónde llegó una línea de trabajo.

Al crear una rama desde el commit actual, inicialmente ambas ramas apuntan al mismo commit:

```text
A ── B ── C
          ↑
          main
          reorganizar-apuntes
```

Los historiales empiezan a diferenciarse cuando registras nuevos commits en una de ellas.

## 4. ¿Qué pasa cuando haces un commit?

Si estás trabajando normalmente en `reorganizar-apuntes` y creas un commit `D`, esa rama avanza para apuntar al nuevo commit:

```text
A ── B ── C ── D
          ↑    ↑
          main reorganizar-apuntes
```

`main` permanece en `C`. El nuevo commit hace avanzar la rama actual, no todas las ramas del repositorio.

Git utiliza una referencia llamada `HEAD` para indicar tu posición actual. En el trabajo habitual sobre una rama, `HEAD` apunta a esa rama. Más adelante veremos también situaciones en las que apunta directamente a un commit.

## 5. ¿Es otra carpeta del proyecto?

Una rama no crea por sí sola una carpeta adicional. Al cambiar de rama en un mismo directorio de trabajo, Git actualiza los archivos según la versión a la que cambias, siempre que pueda hacerlo sin sobrescribir cambios pendientes de forma incompatible.

Por eso conviene consultar `git status` antes de cambiar de rama.

**Los cambios que solo editaste y aún no registraste no quedan automáticamente guardados como historial de una rama.** En algunos casos pueden acompañarte al cambiar de rama; en otros, Git bloqueará el cambio. Para conservar una versión en el historial, necesitas crear un commit.

## 6. ¿Qué significa main?

`main` es un nombre habitual para la rama principal. Git permite usar otros nombres, y algunas ramas principales se llaman `master`.

Git no convierte una rama llamada `main` en una rama especial por su nombre. Su papel principal depende de cómo organice el trabajo el proyecto.

## 7. Crear una rama y cambiar a ella son acciones distintas

Puedes crear una rama sin empezar a trabajar en ella inmediatamente. También puedes usar un comando que haga ambas acciones.

En los siguientes puntos veremos cómo listar, crear y cambiar ramas con comandos como `git branch` y `git switch`.

## Idea principal

**Una rama es un marcador sobre una línea de commits. Te permite desarrollar cambios y decidir después cómo integrarlos con otras líneas de trabajo.**

## Documentación

- [Manual de Git: qué es una rama](https://git-scm.com/docs/user-manual)
- [Modelo de datos de Git](https://git-scm.com/docs/gitdatamodel)
- [Glosario de Git](https://git-scm.com/docs/gitglossary)
