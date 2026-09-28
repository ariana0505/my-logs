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

### Obtener e integrar no significan lo mismo

- **Obtener:** descargar al repositorio local los commits y datos nuevos que están en el remoto. Git ya puede consultarlos, aunque no los estés usando en tu rama actual.
- **Integrar:** incorporar ese historial a tu rama de trabajo mediante una operación como merge o rebase, o mediante un avance directo cuando sea posible.

Git puede almacenar varias versiones del proyecto dentro del repositorio. Descargar una versión no obliga a que tus archivos de trabajo cambien inmediatamente a esa versión.

### Qué cambia después de fetch

| Elemento | Resultado de un fetch normal de origin |
|---|---|
| Datos e historial disponibles localmente | Se obtienen los datos necesarios que faltaban. |
| Referencias de seguimiento como `origin/main` | Se actualizan según lo obtenido y la configuración. |
| Tu rama local `main` | No se integra ni avanza automáticamente. |
| Los archivos en tu carpeta de trabajo | No cambian por esta operación. |
| Tus cambios preparados con `git add` | Permanecen como estaban. |

Si el remoto está en GitHub, necesitas conexión y acceso para obtener sus datos. Una vez descargados, puedes consultar esos commits localmente sin volver a conectarte.

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

### Ejemplo con el contenido de un archivo

Supón que estás en `main` y tu archivo `apuntes.md` contiene:

```text
Estoy aprendiendo Git.
```

Un compañero añade una línea, crea un commit y lo publica en GitHub:

```text
Estoy aprendiendo Git.
Hoy aprendí sobre ramas.
```

Después de ejecutar `git fetch origin`, tu archivo en la carpeta del proyecto sigue teniendo:

```text
Estoy aprendiendo Git.
```

La versión con la línea nueva ya está disponible dentro del repositorio local para consultarla, pero todavía no está integrada en tu rama de trabajo.

**«El archivo sigue igual» se refiere al archivo de tu carpeta del proyecto, esté abierto o cerrado en el editor.** No depende de tener una ventana abierta.

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

En el ejemplo del párrafo nuevo:

- Con fetch, puedes revisar la nueva versión mientras tu archivo de trabajo conserva su contenido.
- Con pull, Git obtiene la nueva versión e intenta incorporarla. Si la integración se completa, tus archivos se actualizan según su resultado.

Pull no significa reemplazar sin más tu proyecto por una copia de GitHub. Intenta integrar historiales; si hay divergencias o conflictos, puede requerir una decisión o intervención.

Puedes pensar en **fetch como «traer la información para revisarla»** y en **pull como «traerla e intentar incorporarla»**.

La integración de pull depende de las opciones, la configuración y el estado de los historiales. Puede avanzar directamente, usar merge o usar rebase.

## 5. ¿Qué pasa con tus cambios pendientes?

Un fetch normal de `origin` no modifica tu directorio de trabajo ni tu área de preparación. Puedes obtener información aunque tengas ediciones pendientes.

Eso no significa que una integración posterior vaya a ser posible con esos mismos cambios pendientes. Revisa `git status` y conserva tu trabajo antes de una operación que necesite actualizar los archivos.

## 6. ¿Fetch obtiene una rama nueva de un compañero?

**Sí, con la configuración habitual, si el compañero la publicó en el remoto que estás consultando.** Si la rama solo existe en su computadora, tu fetch de GitHub no puede obtenerla.

Supón que el compañero creó una rama llamada `nuevo-menu`.

### Paso 1: el compañero publica la rama

En su computadora, ejecuta:

```bash
git push -u origin nuevo-menu
```

Ahora la rama existe en el repositorio remoto compartido. Este comando corresponde al compañero que tiene la rama local, no a ti antes de obtenerla.

### Paso 2: tú obtienes la información del remoto

En tu computadora:

```bash
git fetch origin
git branch -r
```

Puedes ver una salida como:

```text
origin/main
origin/nuevo-menu
```

Git obtuvo los commits necesarios y ahora conoce `origin/nuevo-menu`. **Sigues en tu rama actual y tus archivos no cambian.**

### Paso 3: creas una rama local para trabajar en ella

Si todavía no tienes una rama local llamada `nuevo-menu`, y tus cambios pendientes no impiden cambiar:

```bash
git status
git switch -c nuevo-menu --track origin/nuevo-menu
```

El comando hace tres cosas:

1. Crea tu rama local `nuevo-menu` desde `origin/nuevo-menu`.
2. Configura el seguimiento entre ambas referencias.
3. Cambia tu ubicación de trabajo a la rama local nueva y actualiza los archivos según ella.

Compruébalo con:

```bash
git branch
git status
```

Si la rama local ya existe, usa `git switch nuevo-menu` para cambiar a ella. Un fetch posterior actualiza la referencia de seguimiento; no hace avanzar automáticamente esa rama local existente.

### Los tres lugares de la rama

| Nombre o ubicación | Qué representa |
|---|---|
| `nuevo-menu` en GitHub | La rama publicada en el remoto. |
| `origin/nuevo-menu` en tu repositorio | Tu referencia local de seguimiento de esa rama remota. |
| `nuevo-menu` en tu computadora | Tu rama local, creada para trabajar sobre ese historial. |

Aunque tengan nombres parecidos, son referencias distintas. `origin/nuevo-menu` no es una carpeta nueva ni otra copia visible del proyecto.

```text
Compañero crea nuevo-menu
           ↓ push
GitHub tiene nuevo-menu
           ↓ tu fetch
Tu Git conoce origin/nuevo-menu
           ↓ switch -c ... --track ...
Trabajas en tu rama local nuevo-menu
```

Empezar a trabajar en `nuevo-menu` tampoco integra sus commits en `main`. Cambiar de rama e integrar ramas son operaciones diferentes.

## 7. ¿Siempre obtiene todas las ramas?

Un `git fetch origin` habitual obtiene las ramas del remoto según la configuración de fetch. No actualiza automáticamente otros remotos con nombres diferentes.

Algunos repositorios están configurados para obtener solo determinadas ramas, por ejemplo al clonarse con una selección limitada. En esos casos, una rama nueva puede no aparecer hasta que se obtenga o se configure explícitamente.

Además, estar en `main` al ejecutar fetch no limita la descarga a `main` en la configuración habitual: puedes obtener la información de otras ramas sin cambiar a ellas.

## 8. Ejemplo de consulta con tu proyecto

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

## 9. Dudas frecuentes

| Pregunta | Respuesta |
|---|---|
| ¿Fetch cambia mi archivo abierto en el editor? | No cambia el archivo de trabajo, esté abierto o cerrado. |
| ¿Obtiene los cambios del compañero sin commit ni push? | No. Solo puede obtener datos disponibles en el remoto consultado. |
| ¿Una rama publicada aparece al hacer fetch? | Normalmente sí, como una referencia `origin/nombre`, si la configuración la incluye. |
| ¿Fetch crea una rama local de trabajo por cada rama remota? | No. Puedes crear una cuando quieras trabajar en ella. |
| ¿Fetch me cambia automáticamente a la rama nueva? | No. Para cambiar, usa un comando como `git switch`. |
| ¿Fetch mezcla la rama del compañero con main? | No. Obtener e integrar son pasos distintos. |
| ¿Si una consulta no muestra diferencias, significa que el proyecto es idéntico en todo? | No necesariamente. La consulta tiene un alcance concreto: commits, versiones o rutas, según el comando. |

## Idea principal

**Fetch trae historial y actualiza referencias para que puedas revisarlos. Switch cambia tu rama de trabajo. Pull obtiene historial e intenta integrarlo en tu rama actual.**

## Documentación

- [Referencia oficial de git fetch](https://git-scm.com/docs/git-fetch)
- [Referencia oficial de git pull](https://git-scm.com/docs/git-pull)
- [Referencia oficial de git switch](https://git-scm.com/docs/git-switch)
- [Referencia oficial de git branch](https://git-scm.com/docs/git-branch)
- [Tutorial de Git](https://git-scm.com/docs/gittutorial)
