# Resumen semanal — Semana 1 (S1)

**Fecha de elaboración:** 24/09/2026  
**Registros revisados:** 20/09/2026 al 23/09/2026  
**Estado del resumen:** 🟢 COMPLETO

---

## Resultados de la semana

| Área | Resultado | Estado |
| --- | ---: | --- |
| Inglés | 96/100 | Completado |
| MiniLab 1 — Fundamentos de Git y GitHub | Registro realizado; práctica completa pendiente | Parcial |
| MiniLab 2 — Ramas y conflictos | Registro realizado; conflicto práctico pendiente | Parcial |
| Curso de Claude Code — Módulo 1 | Apuntes registrados | En progreso |
| Curso de Claude Code — Módulos 2, 3 y 4 | Estructura creada; contenido pendiente | Pendiente |

---

## Fuentes utilizadas

- `MiniLab1-2026-09-20.md`
- `MiniLab2-2026-09-20.md`
- Apuntes disponibles en `ClaudeCodeCourse/Modulo1-Introduccion`
- Estructuras creadas para los módulos 2, 3 y 4 de `ClaudeCodeCourse`
- Resultado de inglés informado: 96/100

---

## Todo lo que aprendí

### 1. Fundamentos de Git y GitHub

- Un archivo es una unidad de información que puedo editar y guardar.
- Un repositorio permite que Git lleve el historial de versiones de sus archivos.
- Git funciona localmente y no necesita una conexión permanente con GitHub.
- GitHub permite guardar una copia remota del repositorio.
- Al clonar un repositorio obtengo una copia local y, normalmente, un remoto llamado `origin`.
- Un cambio puede pasar por tres estados principales:
  1. Carpeta de trabajo: el archivo fue editado, pero el cambio todavía no está preparado.
  2. Área de preparación: `git add` selecciona la versión que irá al próximo commit.
  3. Historial: `git commit` registra localmente los cambios preparados.
- `git status` informa el estado de los archivos sin modificarlos.
- `git diff` muestra los cambios que todavía no están preparados.
- `git diff --staged` muestra los cambios que ya fueron preparados.
- `git log --oneline` permite consultar el historial de commits de forma resumida.
- `git add`, `git commit` y `git push` cumplen funciones diferentes:
  - `git add` prepara cambios.
  - `git commit` guarda una versión en el historial local.
  - `git push` envía los commits al repositorio remoto.
- Si corrijo una modificación antes de confirmarla y el archivo vuelve a ser idéntico al último commit, Git deja de mostrarla como un cambio.
- Si vuelvo a editar un archivo después de ejecutar `git add`, puedo tener una versión preparada y otra modificación todavía sin preparar.

### 2. Ramas, fusiones y conflictos

- Un commit pertenece a una historia y una rama es un nombre que apunta a un commit de esa historia.
- Cuando creo un commit nuevo, la rama activa avanza hasta ese commit.
- `git switch -c propuesta` crea una rama desde el punto actual y cambia a ella.
- `git branch --show-current` muestra la rama activa.
- Las ramas permiten desarrollar versiones diferentes sin modificar inmediatamente la rama principal.
- Conviene ejecutar `git status` antes de cambiar de rama para evitar confusiones con cambios pendientes.
- Al ejecutar `git merge propuesta` desde `main`, la rama que recibe la fusión es `main`.
- La dirección de la fusión importa: la rama activa recibe los cambios de la otra rama.
- Un conflicto no significa que Git esté roto. Significa que existen cambios incompatibles que requieren una decisión humana.
- Las marcas `<<<<<<<`, `=======` y `>>>>>>>` separan las versiones que están en conflicto.
- Para resolver un conflicto debo comprender ambas versiones, elegir o redactar el contenido final, borrar las marcas, ejecutar `git add` y guardar la resolución con `git commit`.
- `git log --oneline --graph --all --decorate` permite observar cómo se separaron y volvieron a unirse las historias.

### 3. Claude Code y desarrollo asistido por IA

- El objetivo del curso es usar Claude Code de manera eficiente para aumentar la productividad sin sacrificar calidad.
- El enfoque incluye arquitectura, herramientas, contexto y flujo de desarrollo.
- Claude Code puede utilizarse desde la terminal, una aplicación de escritorio, una extensión de IDE, Slack, Chrome y GitHub Actions.
- El ecosistema de Anthropic incluye productos orientados a programación, atención al cliente, educación, finanzas, salud y seguridad.
- Entre los productos registrados están Claude Code, Claude Code Enterprise, Claude Cowork, Claude Security y las integraciones de Claude para Chrome, Slack, Excel, PowerPoint y Word.

### 4. Agentic loop

- Un agentic loop es un ciclo de trabajo en el que el agente:
  1. Reúne contexto para entender la solicitud y la información necesaria.
  2. Ejecuta una acción, como leer o modificar un archivo.
  3. Verifica el resultado para saber si resolvió el problema.
  4. Ajusta y repite el ciclo cuando todavía existen errores o tareas pendientes.
- El proceso puede resumirse como entender → actuar → comprobar → ajustar.
- Puedo intervenir durante el proceso para orientar el trabajo o establecer límites.

### 5. Modelos y herramientas

- Los modelos reciben una entrada y producen una salida; no conocen automáticamente mi negocio ni conservan por sí solos la memoria del proyecto.
- Según mis apuntes:
  - Opus está orientado al razonamiento y al análisis de problemas complejos.
  - Sonnet busca un equilibrio entre velocidad y calidad, con contexto amplio y ejecución de código.
  - Haiku prioriza la rapidez, la baja latencia y las consultas sencillas o frecuentes.
- Las herramientas permiten que Claude Code realice acciones en la plataforma.
- Entre las herramientas registradas están Agent, Bash, Edit, Skill, WebFetch, WebSearch y Write.

### 6. Contexto, sesiones y memoria

- La ventana de contexto representa la cantidad de tokens que puede procesar la herramienta.
- Las conversaciones, los archivos del proyecto y los resultados de las herramientas pueden formar parte del contexto.
- Cada sesión registra los mensajes y las herramientas utilizadas, lo que permite reanudar conversaciones anteriores.
- Las sesiones están vinculadas a una carpeta.
- Claude Code no conoce automáticamente el flujo de trabajo ni las reglas particulares de un proyecto.
- El archivo `CLAUDE.md` sirve como memoria persistente y permite compartir instrucciones o conocimiento entre sesiones.
- El contexto puede organizarse por alcance:
  - Managed: políticas establecidas por la organización.
  - User: preferencias y configuraciones personales.
  - Project: instrucciones compartidas con el equipo dentro del proyecto.
  - Local: configuraciones específicas de una persona o entorno.

### 7. Agentic Harness y componentes de contexto

- El Agentic Harness permite que Claude Code interactúe con archivos y herramientas de forma autónoma y controlada.
- El sistema de permisos limita qué comandos y archivos puede utilizar el agente.
- El sandbox ofrece un entorno de ejecución controlado para herramientas y scripts.
- El orquestador administra los ciclos de trabajo y las llamadas a herramientas.
- Los principales componentes de contexto registrados son:
  - `CLAUDE.md`: memoria persistente y guía del proyecto.
  - Skills: capacidades modulares y reutilizables.
  - Subagentes: delegación de tareas a agentes especializados.
  - Commands: instrucciones directas que activan flujos concretos.
  - MCPs: integración del modelo con herramientas y fuentes de datos externas.

### 8. Proyecto del curso

- El proyecto propuesto es un álbum con stickers de Cody.
- El usuario podrá marcar qué stickers ya tiene.
- La arquitectura prevista es un monorepo con Turborepo.
- El backend utilizará NestJS.
- El frontend utilizará Next.js.

---

## Lo que comprobé con evidencia

### MiniLab 1

- La rama observada fue `main`.
- El remoto `origin` estaba configurado.
- `README.md`, `file1.txt` y `file2.txt` estaban registrados.
- El árbol de trabajo estaba limpio.
- El historial visible tenía el commit `0789f8a`, «Creando MiniLab1 de Git y Github», fechado el 19/09/2026.
- `main` y `origin/main` apuntaban al mismo commit.

### MiniLab 2

- `estado.txt` contenía «Estado: pendiente».
- La única rama local visible era `main`; `propuesta` todavía no había sido creada.
- El árbol de trabajo estaba limpio.
- El historial visible tenía el commit `052759f`, «Creando MiniLab2 de Git y Github», fechado el 20/09/2026.
- No existían ramas divergentes ni un commit de fusión registrado.

---

## Dificultades y aspectos por revisar

- En el MiniLab 1 no quedó documentada una falla real de Git; solo se identificó una letra «j» suelta en el README.
- En el MiniLab 2 todavía no se ejecutó ni documentó un conflicto real.
- El README del MiniLab 2 contenía «Aver podido» en lugar de «Haber podido».
- Algunos pasos de los ejercicios deben adaptarse porque ambos repositorios ya tienen un commit inicial.
- Los apuntes de instalación de Claude Code contienen comandos fragmentados y deben verificarse antes de ejecutarlos.
- Los módulos 2, 3 y 4 del curso todavía contienen únicamente sus títulos y la sección de objetivos.

---

## Lo que todavía necesito practicar

- Ejecutar en el MiniLab 1 un cambio completo y registrar las salidas reales de `git status`, `git diff` y `git diff --staged`.
- Provocar una errata, verla en el diff, corregirla y comprobar que Git deja de mostrar el cambio cuando el archivo vuelve a su estado anterior.
- Crear la rama `propuesta` en el MiniLab 2.
- Modificar `estado.txt` de forma diferente en `main` y `propuesta`.
- Provocar y resolver un conflicto real de fusión.
- Registrar el mensaje exacto de Git y el historial resultante.
- Completar los contenidos de los módulos 2, 3 y 4 del curso de Claude Code.
- Verificar los comandos de instalación con la documentación oficial antes de utilizarlos.

---

## Próximos pasos

1. Completar la práctica pendiente del MiniLab 1 y añadir evidencia real al log.
2. Ejecutar la práctica de ramas y conflictos del MiniLab 2.
3. Continuar y completar los apuntes de los módulos 2, 3 y 4.
4. Crear un resumen semanal nuevo al finalizar cada semana.
5. Mantener registrados los resultados de evaluaciones, como la nota de inglés `96/100`.

---

## Conclusión semanal

Esta semana aprendí las bases del control de versiones con Git, la diferencia entre preparar, confirmar y publicar cambios, y el funcionamiento inicial de las ramas y los conflictos. También comprendí cómo Claude Code organiza su trabajo mediante un agentic loop, cómo utiliza modelos y herramientas, y por qué el contexto, las sesiones, la memoria y los permisos son importantes. La teoría principal quedó registrada, pero todavía necesito ejecutar las prácticas completas de los dos minilabs y continuar desarrollando los módulos pendientes del curso.
