# 15. git remote y origin

Un **remoto** es una ubicación de otro repositorio con el que intercambias commits. Puede estar alojado en GitHub, en otro servidor o en una ubicación accesible de tu sistema.

`git remote` permite consultar y administrar esas ubicaciones. **`origin` es un nombre habitual para un remoto; no es una rama.**

## 1. Entender origin

Puedes imaginar `origin` como un nombre corto para una dirección:

```text
Repositorio local                   Repositorio remoto
en tu computadora  ←─────────────→  en GitHub
                                    alias: origin
```

El nombre evita tener que escribir la dirección completa cada vez que obtienes o publicas commits.

`origin` no tiene que apuntar a GitHub: el destino depende de la dirección configurada.

## 2. Consultar los remotos

Dentro del repositorio, ejecuta:

```bash
git remote -v
```

Ejemplo de salida:

```text
origin  https://github.com/usuario/proyecto.git (fetch)
origin  https://github.com/usuario/proyecto.git (push)
```

| Parte | Significado |
|---|---|
| `origin` | Nombre del remoto. |
| La URL | Dirección configurada para el repositorio. |
| `(fetch)` | Dirección usada para obtener datos. |
| `(push)` | Dirección usada para publicar datos. |

Las dos direcciones suelen coincidir, aunque Git permite configurarlas de forma diferente. Consultarlas no obtiene ni publica commits.

## 3. Añadir un remoto

En un repositorio que todavía no tenga un remoto llamado `origin`:

```bash
git remote add origin https://github.com/usuario/proyecto.git
```

Reemplaza la URL de ejemplo por la dirección real del repositorio.

Este comando **guarda la configuración del remoto**. No crea el repositorio en GitHub, no envía commits y no descarga su historial.

En tu proyecto `Logs`, `origin` ya está configurado; puedes consultarlo sin volver a añadirlo. Si intentas añadir otro remoto con el mismo nombre, Git mostrará un error.

## 4. Diferencia entre origin y main

| Nombre | Qué representa |
|---|---|
| `origin` | Un remoto configurado: dónde intercambias commits. |
| `main` | Una rama local: una línea de desarrollo. |
| `origin/main` | Una referencia de seguimiento remoto almacenada localmente. |

`origin/main` refleja la información que tu repositorio tiene de esa rama remota; no es una consulta en tiempo real a GitHub.

## 5. Relación con otros comandos

```bash
git push origin main
```

Publica la rama local `main` en la rama `main` del remoto `origin`.

```bash
git pull origin main
```

Obtiene la rama `main` del remoto `origin` e intenta integrarla en tu rama actual. El punto 16 explica estas operaciones con más detalle.

## 6. Ejemplo de consulta en tu proyecto

```bash
cd /Users/ariana/Desktop/Logs
git remote -v
```

Comprueba qué nombres de remoto existen y a qué direcciones apuntan. Esta consulta no modifica tus archivos.

## Idea principal

**`origin` identifica un destino remoto por su nombre. Configurar un remoto y enviar commits a ese remoto son acciones distintas.**

## Documentación

- [Referencia oficial de git remote](https://git-scm.com/docs/git-remote)
- [Tutorial de Git](https://git-scm.com/docs/gittutorial)
