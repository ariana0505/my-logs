# 03. Comandos básicos en la terminal

La **terminal** permite dar instrucciones a la computadora mediante texto. Escribe un comando y presiona **Enter** para ejecutarlo.

Antes de trabajar con Git, conviene aprender a consultar tu ubicación, moverte entre carpetas y manejar archivos. Estos ejemplos sirven para la terminal de tu Mac.

## 1. Entender un comando

Un comando puede tener un nombre, opciones y argumentos:

```bash
ls -l "git y github"
```

| Parte | Función |
|---|---|
| `ls` | Es el comando que lista archivos y carpetas. |
| `-l` | Es una opción que pide una lista con detalles. |
| `"git y github"` | Es el argumento: la carpeta cuyo contenido quieres consultar. |

Las comillas hacen que una ruta con espacios se interprete como un solo argumento. No forman parte del nombre de la carpeta.

## 2. pwd: saber dónde estás

```bash
pwd
```

Muestra la ruta de tu **carpeta actual**, también llamada directorio de trabajo. Por ejemplo:

```text
/Users/ariana/Desktop/Logs
```

Muchos comandos usan esta ubicación como punto de partida. Si un archivo no se encuentra, comprobar tu ubicación con `pwd` puede ayudarte a entender el problema.

## 3. ls: ver archivos y carpetas

```bash
ls
```

Lista el contenido de la carpeta actual.

```bash
ls -a
```

Incluye elementos ocultos, cuyos nombres comienzan con un punto, como `.git`.

```bash
ls -l
```

Muestra detalles como permisos, tamaño y fecha de modificación.

Puedes combinar ambas opciones:

```bash
ls -la
```

## 4. cd: cambiar de carpeta

Si estás en `Logs`, entra en la carpeta de tus apuntes con:

```bash
cd "git y github"
```

Este comando cambia tu ubicación; no mueve ni copia archivos.

Otros movimientos útiles:

| Comando | Resultado |
|---|---|
| `cd ..` | Sube a la carpeta que contiene la actual. |
| `cd ~` | Va a tu carpeta personal. |
| `cd` | También va a tu carpeta personal. |
| `cd -` | Regresa a la ubicación anterior. |

### Rutas absolutas y relativas

Una **ruta absoluta** comienza con `/` e indica una ubicación completa. Puedes usarla desde cualquier carpeta:

```bash
cd "/Users/ariana/Desktop/Logs/git y github"
```

Una **ruta relativa** depende de tu ubicación actual:

```bash
cd "git y github"
```

El segundo ejemplo funciona si la carpeta `git y github` existe dentro de tu carpeta actual.

Atajos para las rutas:

- `.` representa la carpeta actual.
- `..` representa la carpeta que contiene la actual.
- `~` al comienzo de una ruta representa tu carpeta personal.

Por ejemplo, `cd ~/Desktop/Logs` te lleva a `Logs` desde tu carpeta personal.

## 5. mkdir: crear una carpeta

```bash
mkdir practica
```

Crea una carpeta llamada `practica` dentro de la ubicación actual. Para entrar en ella, ejecuta después:

```bash
cd practica
```

Crear la carpeta y entrar en ella son dos acciones distintas.

## 6. cat: leer un archivo de texto

Dentro de `git y github`, ejecuta:

```bash
cat "01 - Qué es Git.md"
```

Muestra el contenido del archivo en la terminal. No lo modifica. Los archivos Markdown se muestran como texto, incluidos sus símbolos de formato, como `#` o `**`.

## 7. cp: copiar un archivo

Dentro de `git y github`, ejecuta:

```bash
cp "01 - Qué es Git.md" "copia.md"
```

El primer argumento es el archivo de origen y el segundo es el destino. Se crea `copia.md` con el contenido del original.

Si ya existe un archivo con el nombre de destino, una copia normal puede sobrescribirlo. Para pedir confirmación antes de sobrescribir, usa:

```bash
cp -i "01 - Qué es Git.md" "copia.md"
```

## 8. mv: mover o renombrar

Para renombrar la copia:

```bash
mv "copia.md" "respaldo.md"
```

Para mover el archivo a una carpeta existente llamada `practica` dentro de tu ubicación actual:

```bash
mv "respaldo.md" practica/
```

El primer argumento es el origen y el segundo es el destino. La opción `-i` también permite pedir confirmación antes de sobrescribir un destino existente.

## 9. Práctica guiada con tus apuntes

Ejecuta estas líneas una por una:

```bash
cd /Users/ariana/Desktop/Logs
pwd
ls
cd "git y github"
pwd
ls
cat "01 - Qué es Git.md"
cd ..
pwd
```

La secuencia permite:

1. Entrar en `Logs`.
2. Comprobar la ubicación y listar su contenido.
3. Entrar en `git y github`.
4. Comprobar la nueva ubicación y listar los apuntes.
5. Leer el archivo del punto 1.
6. Regresar a `Logs` y verificarlo.

Esta práctica consulta archivos y cambia tu ubicación; no crea ni modifica archivos.

## 10. Relación con Git

Estos son comandos de la terminal. Preparan el entorno desde el que ejecutarás comandos de Git, como `git status`, `git add` o `git commit`.

Estar en la carpeta correcta ayuda a que Git opere sobre el repositorio que quieres usar. Git puede encontrar el repositorio desde una subcarpeta del proyecto, por lo que no siempre necesitas estar en su carpeta principal.

## Idea principal

**Primero comprueba dónde estás con `pwd`, consulta el contenido con `ls` y muévete con `cd`.** Con esas tres herramientas puedes ubicarte antes de trabajar con los archivos de un proyecto.

## Documentación

- [Guía de comandos de Apple](https://developer.apple.com/library/archive/documentation/OpenSource/Conceptual/ShellScripting/CommandLInePrimer/CommandLine.html)
- [Cómo especificar rutas en Terminal](https://support.apple.com/en-ca/guide/terminal/apd3cf6fe02-3ec8-48f1-951f-866e52955fc8/mac)
- [Gestión de archivos en Terminal](https://support.apple.com/en-eg/guide/terminal/apddfb31307-3e90-432f-8aa7-7cbc05db27f7/mac)
