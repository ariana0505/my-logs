# 05. git add

`git add` sirve para **preparar el contenido que quieres incluir en el próximo commit**. Lo coloca en el área de preparación, también llamada *staging area* o *index*.

## 1. ¿Cuándo se utiliza?

Después de crear o modificar un archivo y guardarlo en tu editor. También permite preparar la eliminación de un archivo que Git sigue.

Guardar en el editor conserva la edición en el archivo. Ejecutar `git add` selecciona su contenido para el próximo commit. Son acciones distintas.

## 2. Preparar un archivo específico

Desde la carpeta `Logs`:

```bash
git add "git y github/05 - git add.md"
```

Las comillas permiten usar una ruta que contiene espacios.

Si estás dentro de `git y github`, la ruta cambia:

```bash
git add "05 - git add.md"
```

Ambos ejemplos apuntan al mismo archivo desde ubicaciones distintas.

## 3. Preparar varios archivos

```bash
git add archivo1.md archivo2.md
```

Este comando prepara ambos archivos. Puedes ejecutar `git add` varias veces antes de crear un commit.

## 4. Preparar los cambios de la carpeta actual

```bash
git add .
```

El punto representa la carpeta actual. Este comando prepara los cambios dentro de ella y sus subcarpetas: archivos nuevos, modificaciones y eliminaciones.

Git no añade archivos ignorados de forma predeterminada. Más adelante veremos cómo funciona `.gitignore`.

Usa `git status` antes de preparar una carpeta completa para comprobar qué cambios contiene.

## 5. ¿Qué pasa si editas después de preparar?

Imagina esta secuencia:

1. Escribes un primer párrafo y guardas el archivo.
2. Ejecutas `git add`.
3. Escribes un segundo párrafo y vuelves a guardar.

El área de preparación conserva el contenido que existía en el paso 2. Para incluir también el segundo párrafo, debes ejecutar `git add` otra vez.

Por eso un mismo archivo puede tener cambios preparados y cambios sin preparar al mismo tiempo.

## 6. Ejemplo completo

Después de editar y guardar el apunte, desde `Logs`:

```bash
git status
git add "git y github/05 - git add.md"
git status
```

El primer `git status` permite revisar los cambios pendientes. El segundo permite comprobar que el contenido quedó preparado en `Changes to be committed`.

## Idea principal

**`git add` prepara el contenido actual que seleccionas. No crea un commit ni envía cambios a GitHub.**

## Documentación

- [Referencia oficial de git add](https://git-scm.com/docs/git-add)
