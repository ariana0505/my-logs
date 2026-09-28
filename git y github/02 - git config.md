# 02. git config

`git config` sirve para **consultar y modificar la configuración de Git**. Al comenzar, lo más importante es indicar el nombre y el correo que Git registrará como autor de tus commits.

## 1. Configurar tu nombre

Ejecuta en la terminal:

```bash
git config --global user.name "Ariana"
```

Cada parte del comando tiene una función:

| Parte | Significado |
|---|---|
| `git config` | Permite consultar o cambiar la configuración de Git. |
| `--global` | Guarda una configuración para tu usuario de la computadora, disponible en tus repositorios. |
| `user.name` | Es la opción que define el nombre del autor. |
| `"Ariana"` | Es el valor que quieres guardar. Las comillas permiten escribir nombres con espacios. |

Puedes usar tu nombre real o un nombre elegido. No tiene que coincidir con tu nombre de usuario de GitHub.

## 2. Configurar tu correo

```bash
git config --global user.email "tu-correo@example.com"
```

Reemplaza el correo de ejemplo por el que quieras asociar a tus commits antes de ejecutar el comando.

**El nombre y el correo identifican la autoría de los commits; no sirven para iniciar sesión en GitHub ni conceden acceso a un repositorio.**

Normalmente configuras estos datos una vez por usuario de la computadora. No necesitas repetir los comandos antes de cada commit.

## 3. Comprobar los valores que Git utilizará

Dentro de tu repositorio, ejecuta:

```bash
git config --get user.name
git config --get user.email
```

El primer comando muestra el nombre y el segundo muestra el correo efectivos para ese repositorio. Por ejemplo:

```text
Ariana
tu-correo@example.com
```

Si una opción no está configurada, el comando correspondiente puede terminar sin mostrar un valor.

## 4. Configurar solamente un proyecto

Si necesitas usar otra identidad en un proyecto, abre la terminal dentro de ese repositorio y ejecuta:

```bash
git config --local user.name "Ariana"
git config --local user.email "otro-correo@example.com"
```

| Opción | Alcance | Ubicación habitual |
|---|---|---|
| `--global` | Tus repositorios, para tu usuario de la computadora. | `~/.gitconfig` |
| `--local` | Solo el repositorio actual. | `.git/config` |

`~` representa la carpeta personal de tu usuario. Git también admite otras ubicaciones para la configuración global.

**Para estas opciones, el valor local tiene prioridad sobre el global.** Por ejemplo, si tienes un correo personal global y un correo de trabajo local, los nuevos commits de ese proyecto usarán el correo de trabajo.

Si omites `--global` y `--local` al guardar una opción, Git escribe de forma predeterminada en la configuración local. Para escribir allí, debes estar dentro de un repositorio.

## 5. Consultar de dónde viene una configuración

Para revisar el valor y el archivo que lo define:

```bash
git config --show-origin --get user.name
git config --show-origin --get user.email
```

Para listar la configuración disponible:

```bash
git config --list
```

La lista puede incluir otras opciones además del nombre y el correo, como los repositorios remotos.

## 6. ¿Qué pasa si cambias tu nombre o correo?

El cambio se aplica a los **commits futuros**. Los commits anteriores conservan los datos de autoría con los que se crearon.

## Ejemplo para empezar

Sustituye el nombre y el correo por los tuyos:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@example.com"
git config --get user.name
git config --get user.email
```

Los dos primeros comandos guardan los datos y los dos últimos permiten verificarlos. Configurar Git no crea un commit ni sube archivos a GitHub.

## Idea principal

**`git config` define las preferencias de Git. `user.name` y `user.email` indican quién aparecerá como autor de los nuevos commits.**

## Documentación

- [Referencia oficial de git config](https://git-scm.com/docs/git-config)
- [Tutorial oficial de Git](https://git-scm.com/docs/gittutorial)
