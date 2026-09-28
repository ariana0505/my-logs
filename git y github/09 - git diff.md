# 09. git diff

`git diff` permite **consultar las diferencias entre versiones del contenido**. Mientras `git status` te dice qué archivos tienen cambios, `git diff` muestra qué cambió dentro de ellos.

## 1. Consultar los cambios sin preparar

```bash
git diff
```

Sin argumentos, compara el directorio de trabajo con el área de preparación. Muestra modificaciones que todavía no has preparado para el próximo commit.

Los archivos nuevos sin seguimiento no aparecen con su contenido en esta consulta normal. Para identificarlos, usa `git status`.

## 2. Leer las diferencias

Si cambias una línea, puedes ver un fragmento como este:

```diff
-Estoy aprendiendo Git.
+Estoy aprendiendo Git y GitHub.
```

- `-` al comienzo de una línea de contenido indica que esa línea fue eliminada de la versión anterior.
- `+` al comienzo indica una línea añadida en la nueva versión.
- Un espacio inicial indica una línea de contexto sin cambios.

Estos símbolos forman parte de la salida de Git; no se añaden al archivo.

La salida también puede contener encabezados como `--- a/archivo.txt`, `+++ b/archivo.txt` y `@@ ... @@`. Identifican los lados de la comparación y las ubicaciones de los fragmentos; no son líneas eliminadas o añadidas del contenido.

## 3. Consultar los cambios preparados con --staged

```bash
git diff --staged
```

Compara el área de preparación con el último commit. Permite revisar **qué cambios incluirá tu próximo commit normal**.

También puedes escribir:

```bash
git diff --cached
```

En este uso, `--cached` y `--staged` son equivalentes.

| Comando | Comparación | Qué revisa |
|---|---|---|
| `git diff` | Directorio de trabajo frente al área de preparación. | Cambios sin preparar. |
| `git diff --staged` | Área de preparación frente al último commit. | Cambios preparados para el commit. |

Después de `git add`, `git diff` puede quedar vacío porque el archivo de trabajo coincide con su contenido preparado. Eso no significa que no haya cambios para registrar: revísalos con `git diff --staged`.

## 4. Ejemplo de git diff --staged

Este ejemplo supone que `saludo.txt` ya está registrado en el último commit con este contenido:

```text
Hola
```

### Paso 1: editar y guardar

Cambia su contenido por:

```text
Hola, Ariana
```

### Paso 2: preparar el cambio

```bash
git add saludo.txt
```

El área de preparación ahora contiene `Hola, Ariana`.

### Paso 3: revisar lo preparado

```bash
git diff --staged
```

La parte relevante de la salida será:

```diff
-Hola
+Hola, Ariana
```

El próximo commit normal registrará ese reemplazo.

### Paso 4: volver a editar sin preparar

Cambia el archivo y guárdalo así, sin ejecutar otro `git add`:

```text
Hola, Ariana. Bienvenida.
```

Ahora hay tres estados distintos:

| Ubicación | Contenido |
|---|---|
| Último commit | `Hola` |
| Área de preparación | `Hola, Ariana` |
| Archivo de trabajo | `Hola, Ariana. Bienvenida.` |

Por eso `git diff --staged` sigue mostrando:

```diff
-Hola
+Hola, Ariana
```

Mientras que `git diff` muestra:

```diff
-Hola, Ariana
+Hola, Ariana. Bienvenida.
```

**Si haces un commit normal ahora, registrarás `Hola, Ariana`.** Para incluir también `Bienvenida`, prepara otra vez el archivo:

```bash
git add saludo.txt
git diff --staged
```

La comparación preparada mostrará entonces el cambio completo desde `Hola` hasta `Hola, Ariana. Bienvenida.`.

## 5. Revisar un archivo específico

Desde `Logs`, para consultar modificaciones sin preparar del apunte:

```bash
git diff -- "git y github/09 - git diff.md"
```

Para consultar sus modificaciones preparadas:

```bash
git diff --staged -- "git y github/09 - git diff.md"
```

El separador `--` distingue las opciones de la ruta del archivo.

## 6. Secuencia útil antes de un commit

Después de editar y guardar un archivo con seguimiento:

```bash
git status
git diff
git add apuntes.md
git diff --staged
git commit -m "docs: update notes"
```

Sustituye `apuntes.md` por el archivo que quieres registrar. El commit incluye todos los cambios preparados, no solo los de ese archivo.

Si las diferencias se abren en el visor habitual, presiona `q` para salir.

## Idea principal

**`git diff` revisa lo que aún no preparaste; `git diff --staged` revisa lo que ya preparaste para registrar.** Ambos muestran diferencias sin modificar tus archivos ni crear commits.

## Documentación

- [Referencia oficial de git diff](https://git-scm.com/docs/git-diff)
- [Tutorial de Git: diferencias y área de preparación](https://git-scm.com/docs/gittutorial-2)
