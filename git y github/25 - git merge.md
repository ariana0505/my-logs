# 25. git merge

`git merge` permite **integrar el historial de otra rama en la rama donde estás trabajando**.

## 1. Ejemplo sencillo con tus apuntes

Imagina que tienes dos ramas:

- `main`: contiene tus apuntes actuales.
- `mejorar-apuntes`: contiene esos apuntes más una explicación nueva que ya registraste en un commit.

Para incorporar esa explicación a `main`, primero revisa y conserva tu trabajo pendiente. Después:

```bash
git switch main
git merge mejorar-apuntes
```

Es como decir: «Estoy en `main`. Quiero incorporar aquí lo que hice en `mejorar-apuntes`».

```text
mejorar-apuntes ── aporta su historial ──→ main
```

**Primero entra en la rama que recibe; después indica la rama que aporta.** El comando no depende de que la rama receptora se llame `main`.

## 2. Diferencia entre switch y merge

| Comando | Resultado |
|---|---|
| `git switch mejorar-apuntes` | Cambia tu rama de trabajo. |
| `git merge mejorar-apuntes` | Integra esa rama en tu rama actual. |

Cambiar de rama no integra su trabajo en otra. Un merge tampoco elimina automáticamente la rama que aporta los cambios.

## 3. Cuando Git puede avanzar directamente

Si `main` no avanzó por su cuenta desde que se separaron las ramas:

```text
main:              A → B
                        \
mejorar-apuntes:          C → D
```

Una integración habitual puede hacer un **fast-forward**: adelanta `main` hasta `D` sin crear un commit adicional.

```text
A → B → C → D
            ↑
            main
            mejorar-apuntes
```

El resultado puede depender de las opciones de merge y la configuración del proyecto.

## 4. Cuando ambas ramas avanzaron

Si `main` también tiene un commit nuevo:

```text
          E       ← main
         /
A → B
     \
      C → D       ← mejorar-apuntes
```

Un merge normal puede crear un commit de integración `M` que conecta ambos historiales:

```text
A → B → E → M     ← main
     \     /
      C → D       ← mejorar-apuntes
```

Que las ramas tengan commits distintos no significa que necesariamente haya un conflicto: Git puede combinar muchos cambios automáticamente.

## 5. Qué ocurre si hay conflictos

Un conflicto aparece cuando Git no puede decidir automáticamente cómo combinar cambios incompatibles. **La integración se pausa para que decidas el resultado.**

Por ejemplo, ambas ramas cambiaron de formas distintas una misma línea del archivo `apuntes.md`. Al intentar integrar, Git puede insertar estos marcadores. El ejemplo se muestra con sangría:

```text
  <<<<<<< HEAD
  Estoy aprendiendo Git.
  =======
  Estoy aprendiendo Git y GitHub.
  >>>>>>> mejorar-apuntes
```

| Parte | Significado |
|---|---|
| Entre `<<<<<<< HEAD` y `=======` | Contenido de tu lado actual, en este ejemplo `main`. |
| Entre `=======` y `>>>>>>> mejorar-apuntes` | Contenido de la rama que estás integrando. |

Los marcadores delimitan el conflicto; no forman parte del texto final que quieres conservar.

## 6. Resolver el conflicto paso a paso

### Paso 1: consultar los archivos pendientes

```bash
git status
```

Git identifica los archivos sin resolver.

### Paso 2: decidir el contenido final

Abre cada archivo afectado. Puedes elegir una versión o combinar el contenido de ambas ramas. En este ejemplo decides dejar:

```text
Estoy aprendiendo Git y GitHub.
```

Elimina los marcadores `<<<<<<<`, `=======` y `>>>>>>>`, y guarda el archivo. Revisa que el resultado tenga sentido.

### Paso 3: marcar la resolución

```bash
git add apuntes.md
```

Esto prepara el contenido final y marca ese archivo como resuelto. Repite la revisión y preparación para todos los archivos con conflictos.

### Paso 4: completar la integración

```bash
git status
git merge --continue
```

Cuando todas las resoluciones estén preparadas, Git puede crear el commit que completa el merge. Puede abrir un editor para confirmar el mensaje. También se puede finalizar con `git commit` durante esa integración pendiente.

Hay otros tipos de conflictos, como modificar un archivo que la otra rama eliminó; no todos se presentan exactamente con estos marcadores de texto. `git status` ayuda a identificar cada caso.

## 7. Cancelar un merge pendiente

Si prefieres abandonar una integración en curso:

```bash
git merge --abort
```

Intenta reconstruir el estado anterior al merge. No es un comando para deshacer un merge que ya terminó.

Conviene iniciar la integración con el trabajo pendiente conservado: si había modificaciones sin commit antes de empezar y las cambiaste durante el conflicto, abortar no siempre puede reconstruirlas completamente.

## 8. Publicar el resultado

El merge se realiza localmente. Si integraste en `main` y quieres compartir el resultado:

```bash
git push origin main
```

La rama `mejorar-apuntes` sigue existiendo después del merge. Eliminarla, si ya no la necesitas, es una decisión y una operación separadas.

## Idea principal

**Merge integra otra rama en la actual. Si hay conflictos, Git señala el problema, tú decides el contenido, `git add` marca las resoluciones y completas el merge.**

## Documentación

- [Referencia oficial de git merge](https://git-scm.com/docs/git-merge)
- [Manual de Git](https://git-scm.com/docs/user-manual)
