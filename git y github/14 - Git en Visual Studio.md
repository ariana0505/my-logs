# 14. Git en Visual Studio

En este apunte, «Visual Studio» se refiere a **Visual Studio Code (VS Code)**, el editor usado como referencia en la explicación para tu Mac. Visual Studio y Visual Studio Code son productos distintos.

VS Code permite trabajar con Git mediante una interfaz gráfica y una terminal integrada. Los botones realizan operaciones de Git sobre el mismo repositorio que utilizas desde la terminal.

## 1. Preparar el proyecto

Para utilizar la integración, necesitas tener Git instalado y abrir la carpeta de tu proyecto en VS Code.

En tu caso, abre `Logs`, donde ya existe un repositorio. No necesitas inicializar otro para seguir trabajando con tus apuntes.

## 2. Abrir Control de código fuente

Selecciona **Control de código fuente / Source Control** en la barra lateral. Allí puedes consultar los archivos modificados, nuevos y preparados.

El panel separa los cambios sin preparar de los cambios preparados. Los nombres pueden aparecer en español o en inglés según el idioma del editor.

## 3. Revisar las diferencias

Selecciona un archivo en el panel para abrir una comparación de sus cambios.

- En **Changes / Cambios**, consultas los cambios sin preparar.
- En **Staged Changes / Cambios preparados**, consultas el contenido preparado para registrar.

Esto ayuda a revisar qué modificaste antes de crear un commit.

## 4. Preparar un archivo

Coloca el cursor sobre el archivo y pulsa el símbolo **`+`** para preparar sus cambios.

Esta acción corresponde a `git add` sobre ese archivo. También puedes preparar todos los cambios desde el encabezado del grupo, pero conviene revisar cuáles quieres incluir.

Si editas el archivo después de prepararlo, las nuevas modificaciones quedan sin preparar hasta que las selecciones también.

## 5. Crear un commit

Después de preparar y revisar los cambios:

1. Escribe un mensaje, por ejemplo `docs: update Git notes`.
2. Selecciona la acción **Commit** para registrar los cambios preparados.
3. Comprueba si quedan modificaciones pendientes.

Un commit normal registra los cambios preparados en el historial local. Las acciones adicionales de publicación o sincronización pueden variar según la opción elegida y la configuración del editor.

## 6. Publicar y sincronizar

VS Code ofrece acciones para enviar y obtener commits del repositorio remoto.

**Sync Changes / Sincronizar cambios combina pull y push:** primero obtiene e integra los cambios remotos y después publica los commits locales. Si la integración requiere resolver conflictos, tendrás que atenderlos antes de completar la operación.

Por eso, sincronizar es una operación más amplia que ejecutar solamente `git push`.

## 7. Relación con los comandos

| Acción en VS Code | Operación equivalente |
|---|---|
| Consultar archivos modificados | Consultar el estado, como con `git status`. |
| Revisar cambios sin preparar | Comparar contenido, como con `git diff`. |
| Revisar cambios preparados | Comparar lo preparado, como con `git diff --staged`. |
| Preparar un archivo con `+` | `git add archivo`. |
| Registrar los cambios preparados con un mensaje | `git commit -m "mensaje"`. |
| Enviar commits | `git push`. |
| Sincronizar | Obtener e integrar cambios y después enviarlos: pull y push. |

## 8. Ejemplo con tus apuntes

Después de editar y guardar un apunte:

1. Abre Control de código fuente.
2. Selecciona el apunte para revisar sus diferencias.
3. Pulsa `+` junto a ese archivo.
4. Revisa los archivos del grupo de cambios preparados.
5. Escribe un mensaje en inglés que describa la modificación.
6. Crea el commit.
7. Usa la acción de publicación si quieres enviarlo al remoto, o la de sincronización si también quieres obtener e integrar los cambios remotos.

## Idea principal

**VS Code ofrece una interfaz para las operaciones de Git. Preparar, registrar y publicar siguen siendo pasos distintos, aunque los realices con botones.**

## Documentación

- [Tutorial del editor: control de código fuente](https://code.visualstudio.com/docs/getstarted/getting-started)
- [Repositorios y remotos en VS Code](https://code.visualstudio.com/docs/sourcecontrol/repos-remotes)
