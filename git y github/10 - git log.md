# 10. git log

`git log` sirve para **consultar el historial de commits**. Permite conocer las versiones registradas y leer los mensajes que explican los cambios.

## 1. Consultar el historial

Dentro del repositorio, ejecuta:

```bash
git log
```

Sin indicar otras referencias, muestra el historial alcanzable desde tu posición actual, normalmente el último commit de la rama en la que estás trabajando. No muestra automáticamente todos los commits de todas las ramas.

La salida habitual incluye:

- El identificador del commit.
- El nombre y correo del autor.
- La fecha de autoría.
- El mensaje del commit.

Ejemplo ilustrativo:

```text
commit <identificador del commit>
Author: Ariana <tu-correo@example.com>
Date:   <fecha del commit>

    docs: explain Git configuration
```

El identificador permite distinguir y consultar una versión concreta del historial.

## 2. Consultar una vista resumida

```bash
git log --oneline
```

Muestra cada commit en una línea con su identificador abreviado y la primera línea del mensaje.

Ejemplo de commits de este proyecto:

```text
4d8c43d docs: explain git add, status, and commit in separate notes
32315fc docs: explain the Git workflow from editing to pushing
4a34405 docs: explain basic terminal commands and navigation
```

Estos identificadores corresponden a versiones del historial, no a archivos individuales.

## 3. Limitar la cantidad de commits

```bash
git log -5
```

Limita la salida a cinco commits. Puedes combinarlo con la vista resumida:

```bash
git log --oneline -5
```

Esto resulta útil cuando solo quieres revisar las últimas versiones sin recorrer todo el historial.

## 4. Consultar el historial de un archivo

Desde `Logs`, puedes filtrar por la ruta de este apunte:

```bash
git log --oneline -- "git y github/10 - git log.md"
```

El separador `--` indica que lo siguiente es una ruta. Esta consulta se centra en los commits que afectan al archivo según el filtrado del historial de Git.

## 5. Salir del visor

Si Git abre el visor habitual de la terminal para mostrar el historial, presiona:

```text
q
```

Esto cierra la vista y devuelve el control a la terminal. Si toda la salida se muestra directamente sin abrir un visor, no necesitas hacerlo.

## 6. Qué muestra y qué no muestra

`git log` muestra commits ya registrados. No muestra como nuevos commits las ediciones pendientes ni los cambios que solo preparaste con `git add`.

| Comando | Pregunta que ayuda a responder |
|---|---|
| `git status` | ¿Qué archivos tienen cambios pendientes y cuáles están preparados? |
| `git diff` | ¿Qué contenido cambió sin preparar? |
| `git diff --staged` | ¿Qué contenido está preparado para registrar? |
| `git log` | ¿Qué versiones ya quedaron registradas en el historial? |

Puedes consultar el historial local sin conexión a internet. Un commit puede aparecer en `git log` aunque todavía no lo hayas enviado al remoto con `git push`.

## 7. Ejemplo después de un commit

Después de registrar cambios, ejecuta:

```bash
git log --oneline -5
```

Busca el mensaje del commit que acabas de crear. Así puedes comprobar que aparece en el historial local.

Consultar el historial no modifica los archivos ni crea nuevos commits.

## Idea principal

**`git log` permite leer las versiones ya registradas del proyecto.** Los mensajes claros ayudan a entender para qué se creó cada commit.

## Documentación

- [Referencia oficial de git log](https://git-scm.com/docs/git-log)
- [Tutorial de Git](https://git-scm.com/docs/gittutorial)
