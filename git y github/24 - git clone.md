# 24. git clone

`git clone` crea **una copia local de un repositorio existente**, por ejemplo uno alojado en GitHub. Una clonación normal obtiene los archivos y el historial disponible, y deja el proyecto preparado para trabajar con Git.

## 1. Obtener el proyecto en tu computadora

Si estuvieras en otra computadora y quisieras obtener tus apuntes:

```bash
git clone https://github.com/ariana0505/my-logs.git
```

Git crea una carpeta llamada `my-logs` dentro de tu ubicación actual. Después entra en ella y consulta el estado:

```bash
cd my-logs
git status
```

Ejecuta clone desde la carpeta donde quieras guardar esa copia. En tu carpeta actual `Logs` ya tienes el repositorio: no necesitas clonarlo otra vez para actualizarlo.

## 2. Qué configura automáticamente

En una clonación habitual, Git:

- Crea la carpeta del proyecto y su repositorio `.git`.
- Obtiene los datos y el historial disponibles según las opciones de clonación.
- Prepara una rama inicial, normalmente la predeterminada del remoto.
- Configura `origin` con la dirección desde la que clonaste.
- Configura el seguimiento de la rama inicial.

Por eso puedes consultar el remoto con:

```bash
git remote -v
```

Y obtener e integrar actualizaciones posteriores con:

```bash
git pull
```

Una copia local es un repositorio con su propio historial y referencias, no solo una descarga de archivos. Las opciones especiales, como una clonación superficial, pueden limitar el historial obtenido.

## 3. Elegir el nombre de la carpeta

```bash
git clone https://github.com/ariana0505/my-logs.git mis-apuntes
```

En este caso, la carpeta se llama `mis-apuntes`. El último argumento indica el destino local; no cambia el nombre del repositorio en GitHub.

## 4. Qué ocurre con las otras ramas

Una clonación habitual obtiene referencias de seguimiento de las ramas remotas. Puedes consultarlas con:

```bash
git branch -r
```

No crea una rama local de trabajo por cada rama remota. Para empezar a trabajar en una rama obtenida, si todavía no existe localmente:

```bash
git switch -c nuevo-menu --track origin/nuevo-menu
```

Este ejemplo requiere que `origin/nuevo-menu` exista. Crea una rama local con seguimiento y cambia a ella.

## 5. Diferencia con fetch y pull

| Comando | Uso |
|---|---|
| `git clone` | Crea una copia local nueva de un repositorio. |
| `git fetch` | Obtiene actualizaciones en una copia existente sin integrarlas en tu rama. |
| `git pull` | Obtiene actualizaciones e intenta integrarlas en tu rama actual. |

No vuelvas a clonar cada vez que alguien publique cambios. Actualiza la copia que ya tienes.

## 6. Acceso y publicación

Para clonar desde GitHub necesitas conexión y acceso al repositorio. Un repositorio privado requiere autenticación y autorización.

Poder clonar un proyecto no significa que tengas permiso para publicar cambios en él. Puedes editar y crear commits localmente; publicar requiere permisos en el remoto de destino.

## Idea principal

**Clone obtiene una copia nueva del proyecto y su repositorio. Fetch y pull actualizan una copia que ya existe.**

## Documentación

- [Referencia oficial de git clone](https://git-scm.com/docs/git-clone)
- [Tutorial de Git](https://git-scm.com/docs/gittutorial)
