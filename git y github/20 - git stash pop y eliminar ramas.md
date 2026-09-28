# 20. git stash pop y eliminar ramas

Este punto contiene dos operaciones distintas: **recuperar trabajo guardado en el stash** y **eliminar una rama local que ya no necesitas**.

## 1. ¿Qué hace git stash pop?

```bash
git stash pop
```

Aplica el stash más reciente en tu ubicación de trabajo actual. Si se aplica correctamente, elimina su entrada de la lista de stashes.

Los cambios recuperados vuelven como trabajo pendiente. El comando no crea automáticamente un commit en tu rama.

## 2. ¿Qué significa «entrada del stash»?

Una **entrada** es un guardado temporal que aparece en:

```bash
git stash list
```

Por ejemplo:

```text
stash@{0}: On mejorar-apuntes: Work in progress on Git notes
```

Esta línea representa un guardado de tus cambios. `stash@{0}` identifica el más reciente; no es el archivo donde estabas escribiendo.

Piensa en el stash como un cajón donde guardas temporalmente trabajo pendiente.

## 3. Diferencia entre apply y pop

Supón que agregaste un párrafo a un archivo con seguimiento y guardaste ese trabajo con:

```bash
git stash push -m "Save unfinished paragraph"
```

El párrafo deja de aparecer en el archivo de trabajo y queda guardado en el stash.

### Si eliges git stash apply

```bash
git stash apply
```

- El párrafo vuelve al archivo.
- El guardado permanece en `git stash list`.

Es como **sacar una copia de un cajón y dejar el original dentro**. Puedes seguir trabajando con lo recuperado y todavía conservas el guardado temporal.

### Si eliges git stash pop

```bash
git stash pop
```

- El párrafo vuelve al archivo.
- Si se aplica correctamente, ese guardado deja de aparecer en `git stash list`.

Es como **sacar lo guardado del cajón y dejar ese espacio vacío**.

**`pop` no borra los cambios recuperados del archivo. Elimina únicamente la entrada temporal del stash después de aplicarla correctamente.** Si tienes otras entradas, estas permanecen en la lista.

Los ejemplos con `apply` y `pop` son alternativas para entender la diferencia. No necesitas ejecutar ambos sobre el mismo guardado para recuperarlo.

## 4. Comparación visual

```text
Antes de recuperar:
    Archivo: sin el párrafo pendiente
    Stash:   guardado con el párrafo

Después de apply, si se aplica correctamente:
    Archivo: con el párrafo recuperado
    Stash:   conserva el guardado

Después de pop, si se aplica correctamente:
    Archivo: con el párrafo recuperado
    Stash:   ya no contiene ese guardado
```

## 5. ¿Qué pasa si hay conflictos?

Si Git no puede combinar los cambios guardados con el contenido actual, puede aplicar parte del trabajo y señalar conflictos.

En ese caso, **`git stash pop` conserva la entrada**. Consulta `git status`, revisa los archivos y resuelve los conflictos.

Después de comprobar que recuperaste el trabajo correctamente, puedes eliminar la entrada que ya no necesites con `git stash drop`. Revisa primero `git stash list` para identificarla.

No vuelvas a ejecutar `pop` sobre cambios parcialmente aplicados suponiendo que no ocurrió nada: revisa el estado antes de continuar.

## 6. Ejemplo al retomar tus apuntes

Supón que guardaste trabajo de `mejorar-apuntes` en el stash más reciente y luego cambiaste a `main`. Cuando quieras retomarlo, después de conservar cualquier otro trabajo pendiente:

```bash
git status
git switch mejorar-apuntes
git stash list
git stash pop
git status
```

Los cambios vuelven a tu ubicación de trabajo en `mejorar-apuntes`. Revísalos antes de prepararlos y registrarlos con `git add` y `git commit`.

Si tienes varias entradas, puedes elegir una explícitamente:

```bash
git stash pop 'stash@{0}'
```

Las comillas pasan la referencia como un argumento literal. Sustituye el índice por el de la entrada que corresponda tras consultar la lista.

## 7. Eliminar una rama local

Cuando una rama ya cumplió su función, puedes eliminarla. Primero cambia a otra rama:

```bash
git status
git switch main
git branch -d mejorar-apuntes
```

Este ejemplo supone que `main` existe y que puedes cambiar a ella sin interferir con trabajo pendiente.

No puedes eliminar una rama activa en un directorio de trabajo, incluido otro worktree del mismo repositorio.

`-d` comprueba que la rama esté completamente integrada en su rama de seguimiento o, si no tiene seguimiento configurado, en tu posición actual (`HEAD`). Si no cumple esa condición, Git rechaza la eliminación.

## 8. Eliminar una rama de forma forzada

```bash
git branch -D mejorar-apuntes
```

La `D` mayúscula fuerza la eliminación aunque la rama tenga commits sin integrar. Úsala cuando hayas decidido descartar esa referencia.

Eliminar la rama quita su nombre del repositorio; no deshace cambios que ya estén integrados en otras ramas. Sin embargo, puedes perder el acceso habitual a commits que solo eran alcanzables por la rama eliminada.

Eliminar una rama local no elimina automáticamente la rama correspondiente en GitHub. Son referencias distintas.

## Resumen

| Comando | Resultado |
|---|---|
| `git stash apply` | Recupera los cambios y conserva la entrada guardada. |
| `git stash pop` | Recupera los cambios y elimina la entrada si logra aplicarla correctamente. |
| `git stash list` | Lista los guardados temporales disponibles. |
| `git branch -d nombre` | Elimina una rama local si supera la comprobación de integración. |
| `git branch -D nombre` | Fuerza la eliminación de una rama local sin esa comprobación. |

## Idea principal

**`pop` recupera tu trabajo y, si tiene éxito, retira su guardado temporal. Eliminar una rama es otra operación: quita una referencia del historial, no un stash.**

## Documentación

- [Referencia oficial de git stash](https://git-scm.com/docs/git-stash)
- [Referencia oficial de git branch](https://git-scm.com/docs/git-branch)
