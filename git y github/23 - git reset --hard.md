# 23. git reset --hard

`git reset --hard` **ajusta la rama actual, el área de preparación y los archivos de trabajo al commit de destino**. Si no indicas un destino, utiliza el commit actual.

A diferencia del reset predeterminado, no conserva las modificaciones pendientes de los archivos con seguimiento.

## 1. Retroceder un commit y restaurar esa versión

Supón que tienes este historial lineal y no hay ediciones pendientes:

```text
A → B → C   ← rama actual
```

Con:

```bash
git reset --hard HEAD~1
```

La rama pasa a apuntar a `B`, y el área de preparación y los archivos se ajustan a la versión registrada en `B`.

| Elemento | Antes | Después |
|---|---|---|
| Rama actual | Apunta a `C`. | Apunta a `B`. |
| Área de preparación | Coincide con `C`. | Coincide con `B`. |
| Archivos de trabajo | Contienen la versión de `C`. | Contienen la versión de `B`. |

`HEAD~1` indica el primer padre del commit actual. En este historial lineal, es el commit anterior.

## 2. Ejemplo con el contenido de un archivo

En el commit `B`, `apuntes.md` tenía:

```text
Estoy aprendiendo Git.
```

En el commit `C`, agregaste:

```text
Estoy aprendiendo Git.
Hoy aprendí sobre ramas.
```

Si haces `git reset --hard HEAD~1` desde `C`, el archivo vuelve a contener:

```text
Estoy aprendiendo Git.
```

La segunda línea deja de estar en tu archivo de trabajo porque estás restaurando el estado de `B`.

## 3. Qué pasa con las modificaciones pendientes

Si después de `C` escribiste otro párrafo sin registrarlo, ese trabajo también se descarta al ajustar el archivo al destino.

**Antes de usar `--hard`, conserva cualquier trabajo que necesites.** Puedes registrarlo en un commit, guardarlo temporalmente en un stash adecuado o hacer una copia fuera de los archivos que se ajustarán.

Una rama de respaldo conserva un commit, pero no guarda por sí sola ediciones pendientes. Además, un stash normal no incluye archivos nuevos sin seguimiento; revisa qué necesitas conservar.

## 4. Usar --hard sin indicar otro commit

```bash
git reset --hard
```

Equivale a:

```bash
git reset --hard HEAD
```

La rama no retrocede porque el destino es el commit actual. El comando ajusta el área de preparación y los archivos a ese commit, descartando sus diferencias locales.

Por tanto, **`--hard` no significa automáticamente «retroceder un commit»**. Retroceder depende del destino que indiques.

## 5. Diferencia con git reset

Para el mismo destino:

| Comando | Rama | Archivos de trabajo |
|---|---|---|
| `git reset HEAD~1` | Retrocede al padre. | Conservan el contenido anterior al comando. |
| `git reset --hard HEAD~1` | Retrocede al padre. | Se ajustan al contenido del padre. |

Ambos ajustan el área de preparación al destino. La diferencia principal en estos ejemplos es lo que ocurre con el contenido de los archivos.

## 6. Archivos sin seguimiento

`--hard` no debe entenderse como un comando que elimina indiscriminadamente todos los archivos nuevos. Sin embargo, **puede sobrescribir o eliminar archivos sin seguimiento que interfieran con la restauración del destino**.

Los archivos que Git sigue y que no existen en el commit de destino se retiran para que el estado de trabajo coincida con ese commit.

No uses la presencia de archivos sin seguimiento como garantía de que permanecerán intactos ante cualquier reset hard.

## 7. Revisar antes de decidir

Estas consultas permiten entender qué tienes antes de ejecutar una operación de descarte:

```bash
git status
git diff
git diff --staged
git log --oneline -5
```

Muestran el estado, los cambios sin preparar, los cambios preparados y los commits recientes. Los archivos nuevos sin seguimiento se identifican con `git status`; su contenido no aparece en un diff normal.

Los comandos de reset de este apunte son ejemplos para comprender su efecto, no pasos que debas ejecutar sobre trabajo que quieres conservar.

## 8. Relación con GitHub y recuperación

El reset afecta al repositorio local. No cambia automáticamente las ramas publicadas en GitHub.

Si el commit ya está compartido, normalmente conviene deshacer sus cambios con `git revert` para conservar el historial compartido.

Los commits que dejaron de estar en la rama pueden seguir disponibles mediante otras referencias o registros locales. Eso no garantiza recuperar modificaciones que nunca se registraron ni se guardaron. Conserva el trabajo antes de descartarlo.

## Idea principal

**`git reset --hard` hace que la preparación y los archivos coincidan con el commit elegido. Puede descartar trabajo pendiente; el destino determina si la rama retrocede o permanece en el mismo commit.**

## Documentación

- [Referencia oficial de git reset](https://git-scm.com/docs/git-reset)
- [Referencia oficial de git revert](https://git-scm.com/docs/git-revert)
