# 21. git fetch

`git fetch` permite **obtener commits e información de un repositorio remoto sin integrarlos automáticamente en tu rama de trabajo**.

Es útil cuando quieres conocer los cambios publicados por otras personas o desde otra computadora antes de decidir cómo incorporarlos.

## 1. Obtener información del remoto

Dentro del repositorio:

```bash
git fetch origin
```

`origin` es el nombre del remoto. Con la configuración habitual, Git descarga los datos necesarios y actualiza las referencias de seguimiento remoto, como `origin/main`.

**Este comando no integra los cambios en tu rama local `main` ni modifica tus archivos de trabajo.** Sí actualiza información dentro del repositorio local, por lo que obtener datos es distinto de solo consultar una lista.

## 2. Ejemplo con el historial

Supón que tu computadora tiene los commits `A` y `B`, pero alguien ya publicó un commit `C` en GitHub:

```text
Tu main:         A ── B
GitHub main:     A ── B ── C
```

Después de `git fetch origin`, tu repositorio conoce el commit `C`:

```text
main:            A ── B
origin/main:     A ── B ── C
```

| Referencia | Qué indica en este ejemplo |
|---|---|
| `main` | Tu rama local, que todavía apunta a `B`. |
| `origin/main` | La referencia local de seguimiento remoto, actualizada para apuntar a `C`. |

El contenido de tus archivos sigue correspondiendo a tu posición local y a las ediciones pendientes que pudieras tener. Conocer `C` no significa que ya lo hayas integrado.

## 3. Revisar los commits obtenidos

Si quieres comparar tu historial actual con `origin/main`:

```bash
git log --oneline HEAD..origin/main
```

Muestra los commits alcanzables desde `origin/main` que no están en el historial alcanzable desde tu posición actual, `HEAD`.

En el ejemplo anterior, mostraría el commit `C`. Si no hay commits en ese rango, no mostrará ninguna línea.

Para revisar las diferencias de contenido entre ambas versiones registradas:

```bash
git diff HEAD origin/main
```

Esta comparación usa el commit actual y el de `origin/main`; no incluye tus ediciones pendientes sin registrar.

Antes de comparar, comprueba que estás en la rama que quieres revisar. Comparar una rama de una función con `origin/main` puede mostrar diferencias más amplias que las de una actualización pendiente de `main`.

## 4. Diferencia entre fetch y pull

| Comando | Qué hace |
|---|---|
| `git fetch origin` | Obtiene datos y actualiza referencias de seguimiento remoto según la configuración, sin integrar en tu rama actual. |
| `git pull` | Obtiene datos y después intenta integrar la rama remota correspondiente en tu rama actual. |

Puedes pensar en **fetch como «traer la información para revisarla»** y en **pull como «traerla e intentar incorporarla»**.

La integración de pull depende de las opciones, la configuración y el estado de los historiales. Puede avanzar directamente, usar merge o usar rebase.

## 5. ¿Qué pasa con tus cambios pendientes?

Un fetch normal de `origin` no modifica tu directorio de trabajo ni tu área de preparación. Puedes obtener información aunque tengas ediciones pendientes.

Eso no significa que una integración posterior vaya a ser posible con esos mismos cambios pendientes. Revisa `git status` y conserva tu trabajo antes de una operación que necesite actualizar los archivos.

## 6. Ejemplo de consulta con tu proyecto

Desde `Logs`:

```bash
cd /Users/ariana/Desktop/Logs
git status
git branch
git fetch origin
git log --oneline HEAD..origin/main
git diff HEAD origin/main
```

Este ejemplo supone que quieres comparar tu posición actual con `origin/main`, que el remoto está configurado y que esa referencia existe.

La secuencia permite revisar el estado y la rama actual, actualizar la información remota, consultar commits que no están en tu historial actual y comparar las versiones registradas.

Después de fetch, decides si quieres integrar los cambios. Fetch por sí solo no hace avanzar tu rama local.

## Idea principal

**`git fetch` actualiza tu conocimiento del repositorio remoto. Te permite revisar los cambios antes de incorporarlos a tu rama.**

## Documentación

- [Referencia oficial de git fetch](https://git-scm.com/docs/git-fetch)
- [Referencia oficial de git pull](https://git-scm.com/docs/git-pull)
- [Tutorial de Git](https://git-scm.com/docs/gittutorial)
