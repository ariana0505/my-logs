# 19. git stash

`git stash` permite **guardar temporalmente cambios pendientes** y retirarlos de tu ubicación de trabajo para continuar con otra tarea.

Es útil cuando necesitas cambiar de rama, pero tu trabajo todavía no está listo para registrarse como un commit en esa rama.

## 1. Guardar el trabajo pendiente

Dentro del repositorio:

```bash
git stash push -m "Work in progress on Git notes"
```

El comando guarda las modificaciones preparadas y sin preparar de los archivos que Git ya sigue. Después, en su uso habitual, devuelve esos archivos y el área de preparación al estado del commit actual.

`-m` permite añadir un mensaje para reconocer lo que guardaste.

También puedes usar la forma breve:

```bash
git stash
```

Para empezar, la forma con `push -m` ayuda a describir cada guardado.

## 2. Incluir archivos nuevos sin seguimiento

Por defecto, el stash no incluye los archivos nuevos que Git todavía no sigue. Para incluirlos junto con los cambios de archivos con seguimiento:

```bash
git stash push -u -m "Work in progress on Git notes"
```

`-u` equivale a `--include-untracked`. Los archivos nuevos incluidos se guardan en el stash y se retiran del directorio de trabajo hasta que los recuperes.

**`-u` no incluye archivos ignorados.** Por eso, después del guardado, consulta `git status` para comprobar qué trabajo sigue pendiente.

## 3. Consultar los cambios guardados

```bash
git stash list
```

Ejemplo de salida:

```text
stash@{0}: On mejorar-apuntes: Work in progress on Git notes
```

`stash@{0}` representa la entrada más reciente. Si guardas más trabajo, las entradas anteriores cambian de posición en la lista.

El nombre de la rama en el mensaje sirve como referencia del contexto en que guardaste los cambios; no obliga a recuperarlos exclusivamente en esa rama.

## 4. Recuperar cambios conservando la entrada

```bash
git stash apply
```

Aplica el stash más reciente en tu directorio de trabajo actual y conserva su entrada en la lista.

Para elegir una entrada concreta:

```bash
git stash apply 'stash@{0}'
```

Las comillas permiten pasar la referencia como un argumento literal a la terminal.

Aplicar un stash no crea un commit en tu rama. Los cambios vuelven como trabajo pendiente para que puedas revisarlos, prepararlos y registrarlos cuando corresponda.

## 5. Recuperar el estado de preparación

El stash guarda información del área de preparación, pero un `apply` normal no necesariamente restaura qué cambios estaban preparados.

Si también quieres intentar recuperar ese estado:

```bash
git stash apply --index
```

La restauración puede fallar si hay conflictos. Consulta `git status` después para comprobar el resultado.

## 6. Ejemplo al cambiar de rama

Supón que estás en `mejorar-apuntes`, tienes cambios pendientes y necesitas trabajar en `main`:

```bash
git status
git stash push -u -m "Work in progress on Git notes"
git status
git switch main
```

Cuando hayas terminado y conservado el trabajo realizado en `main`, regresa y recupera el stash:

```bash
git switch mejorar-apuntes
git stash apply
git status
```

Este ejemplo supone que no creaste otro stash entretanto. Si tienes varias entradas, consulta `git stash list` y elige la que corresponda.

## 7. Conflictos y almacenamiento local

Si el contenido actual es incompatible con los cambios guardados, aplicar el stash puede producir conflictos. Debes revisar el resultado y resolverlos antes de continuar con tu trabajo.

El stash se guarda localmente. Un push normal no publica sus entradas en GitHub.

`apply` conserva la entrada incluso después de aplicar los cambios correctamente. En el punto 20 veremos `git stash pop`, que elimina la entrada cuando logra aplicarla sin conflictos.

## Idea principal

**`git stash` guarda temporalmente trabajo pendiente. `git stash apply` lo recupera y conserva la entrada guardada.** No sustituye el registro y la publicación de versiones mediante commits y push.

## Documentación

- [Referencia oficial de git stash](https://git-scm.com/docs/git-stash)
- [Manual de Git](https://git-scm.com/docs/user-manual)
