# CONCEPTOS

(23/09/2026)

---

## Objetivos de la clase 🎯

Entender el agent loop y cómo funciona Claude Code.

---

## 1 - ¿Qué es un agentic loop?

![alt text](image.png)

Imagina que le dices a Claude Code: «Ayúdame a resolver un problema en mi proyecto».

Según el diagrama, ocurre lo siguiente:

---

### AGENTIC LOOP

- Gather context — reunir contexto: lee tu pedido y revisa la información necesaria.

- Take action — actuar: decide qué paso dar y lo realiza; por ejemplo, modifica un archivo.

- Verify results — verificar resultados: comprueba si esa acción resolvió el problema.

Si todavía hay un error, vuelve a reunir contexto y repite el ciclo. Cuando verifica que cumplió el objetivo, llega a Done.
 
---

Tú también puedes intervenir en cualquier momento para orientar el trabajo: «Revisa este archivo» o «No cambies esa parte». Claude Code incorpora esa información en los siguientes pasos.

En pocas palabras: un agentic loop es el ciclo entender → actuar → comprobar → ajustar que un agente repite mientras trabaja en un objetivo.

### Modelos

Los modelos son el corazón del desarrollo asistido por AI.

Estos solo reciben una entrada y entregan una salida.

No tienen memoria; no conocen tu negocio.

Algunos modelos disponibles en Claude:

1. Modelo Opus (Potencia Extrema)

   Características:

   - Razonamiento Superior
   - Análisis de Datos Complejos
   - Resolución de Problemas

2. Modelo Sonnet (Equilibrio Rendimiento)

   Características:

   - Velocidad y Calidad
   - Contexto Amplio
   - Ejecución de Código

3. Modelo Haiku (Rapidez Ágil)

   Características:

   - Latencia Mínima
   - Tareas de Alta Frecuencia
   - Consultas Sencillas

### Tools

Es software que le permite a Claude Code realizar acciones sobre la plataforma.

Algunas de las herramientas que son parte de Claude Code:

- Agent
- Bash
- Edit
- Skill
- WebFetch
- WebSearch
- Write

#### En profundidad

El modelo por sí solo únicamente piensa en texto: recibe palabras y devuelve palabras. No puede, por su cuenta, tocar un archivo en el disco ni ejecutar un comando. Las tools son lo que rompe esa limitación: son piezas de software que el modelo puede invocar cuando decide que necesita hacer algo concreto en el mundo real.

Dentro del agentic loop, en el paso «Take action», el modelo no actúa directamente: dice qué herramienta quiere usar y con qué parámetros, y el Agentic Harness es quien la ejecuta de verdad y devuelve el resultado.

- **Bash**: ejecuta comandos de terminal; es la más versátil.
- **Edit**: modifica una parte de un archivo existente sin reescribirlo completo.
- **Write**: crea un archivo nuevo o lo reemplaza por completo.
- **WebFetch / WebSearch**: traen información desde internet.
- **Agent**: lanza un subagente para que resuelva una parte del trabajo por separado.
- **Skill**: activa un paquete de instrucciones predefinido para una tarea específica.

Cada tool tiene un propósito y unos parámetros propios; el modelo decide cuál usar según lo que necesite lograr en ese paso del loop.

### Ventana de contexto

Es la cantidad de tokens que puede procesar la herramienta.

Las conversaciones que tenemos, los archivos del proyecto y las herramientas que usamos: todo esto es o puede ser parte del
contexto.

![alt text](image-1.png)

#### En profundidad

La ventana de contexto funciona como la memoria RAM del modelo mientras trabaja, no como almacenamiento permanente. Todo lo que «tiene presente» en un momento dado cuenta contra un límite fijo de tokens (un token es aproximadamente un pedacito de palabra).

Qué entra ahí:

- Todo el historial de mensajes de la sesión actual.
- El contenido de los archivos que se han leído.
- Los resultados de las herramientas que se han ejecutado.
- Instrucciones de sistema, memoria de `CLAUDE.md`, skills activas, etc.

Por qué importa:

- Si la conversación se alarga mucho o se leen archivos muy grandes, la ventana se puede llenar; cuando eso pasa, el sistema resume o descarta lo más antiguo para hacer espacio.
- Por eso a veces conviene ser selectivo: leer solo la parte relevante de un archivo en lugar del archivo completo.
- No es memoria persistente: cuando la sesión termina o se resume, ese contenido puede perderse, a diferencia de lo que se guarda en `CLAUDE.md`.

En resumen: las tools son las manos del modelo, y la ventana de contexto es cuánto puede recordar activamente mientras las usa.

### Sesión

Cada vez que abrimos Claude Code, se genera una sesión; en esta se guarda cada mensaje y las herramientas usadas.

Esto permite reanudar una conversación anterior.

Las sesiones están ligadas a una carpeta.

![alt text](image-2.png)

#### En profundidad

Una sesión no es solo «una conversación abierta»: es un objeto que Claude Code guarda en disco con todo su historial.

- Cada mensaje y cada respuesta, incluyendo qué herramientas se usaron y qué resultado dieron, queda registrado dentro de esa sesión.
- La sesión queda ligada a la carpeta desde la que se ejecutó `claude`. Eso permite cerrar la terminal, volver más tarde, entrar a la misma carpeta y reanudar exactamente donde se quedó, sin repetir el contexto del proyecto.
- Abrir Claude Code en una carpeta distinta es técnicamente otra sesión, aunque sea carpeta hija o hermana de la anterior.

Es la memoria de corto plazo de una conversación específica, distinta de la memoria persistente que da `CLAUDE.md`.

### Agentic Harness

Permite a Claude Code interactuar de forma autónoma y segura con el sistema de archivos y las herramientas del entorno local.

- Permission System: Control granular sobre qué comandos y archivos puede tocar el agente.

- Tool Sandbox: Ejecución segura de herramientas CLI y scripts en el entorno del usuario.

- Orchestrator: Gestión de ciclos de pensamiento y llamadas a herramientas.

#### En profundidad

Es el sistema que hace posible actuar sobre la computadora sin que sea peligroso o descontrolado. Sus tres piezas trabajan juntas:

- **Permission System**: filtra qué se puede hacer sin pedir aprobación explícita. Leer un archivo suele estar permitido libremente; borrar archivos o hacer `git push` normalmente requiere confirmación. Es configurable: se puede decidir qué comandos quedan siempre permitidos o siempre bloqueados.
- **Tool Sandbox**: el entorno real, aislado y controlado, donde se ejecutan los comandos pedidos, para que un error quede contenido ahí.
- **Orchestrator**: el «director de orquesta» que decide cuándo le toca al modelo pensar, cuándo llamar a una herramienta, cuándo pedir permiso, y cuándo el ciclo (el agentic loop) ya terminó.

Idea central: el modelo por sí solo solo genera texto; el Harness convierte ese texto en acciones reales y seguras sobre el sistema.

---

## 2 - Arquitectura

### Memoria

Claude Code no conoce nuestro flujo de trabajo; hay muchos detalles de nuestra operación que no conoce.

Para poder darle información a Claude Code usamos un archivo llamado `CLAUDE.md`. Con esto, el conocimiento estará disponible para todas las sesiones.

Estos archivos se organizan por scope.

#### En profundidad

Diferencia clave entre memoria de sesión y memoria persistente:

- Una sesión se olvida cuando se cierra, salvo que se reabra en la misma carpeta.
- `CLAUDE.md` es distinto: es un archivo de texto que se escribe una vez, y su contenido se carga automáticamente al inicio de cada sesión nueva que se abra en esa carpeta o en sus subcarpetas. No hace falta repetir el contexto del proyecto cada vez.

### Scope

Permite definir la jerarquía de configuraciones y contexto que se aplica en la sesión.

- Managed: políticas que define la organización.

- User: preferencias personales y configuraciones personales.

- Project: configuraciones por proyecto y compartidas con el equipo.

- Local: configuraciones específicas para el usuario.

#### En profundidad

El scope define en qué nivel vive un `CLAUDE.md`, y por lo tanto a quién y a qué proyectos aplica, de lo más general a lo más específico:

| Scope | Quién lo define | Ejemplo |
| --- | --- | --- |
| Managed | La organización | Reglas de seguridad que no se pueden cambiar |
| User | La persona usuaria, para todos sus proyectos | «Responder siempre en español» |
| Project | Compartido con el equipo en ese proyecto | «Este repo usa NestJS y Next.js» |
| Local | Solo la persona usuaria, solo en esa carpeta | Configuraciones que no se comparten si el repo se sube a GitHub |

Si hay conflicto entre niveles, normalmente gana el nivel más específico.

### Contexto

| Componente | Rol en la arquitectura de contexto |
| --- | --- |
| `CLAUDE.md` | Memoria persistente y guía de estilo para el proyecto. |
| Skills | Capacidades modulares y herramientas reutilizables. |
| Subagentes | Delegación de tareas complejas a procesos especializados. |
| Commands | Instrucciones directas y disparadores de flujos específicos. |
| MCPs | Protocolo de Contexto Modelo para integración de datos externos. |

#### En profundidad

Formas de dar «conocimiento o capacidades» a Claude Code más allá de lo escrito en el chat:

- **`CLAUDE.md`**: memoria persistente en texto plano.
- **Skills**: paquetes de instrucciones ya armados para una tarea específica, en lugar de explicar todo el procedimiento desde cero cada vez.
- **Subagentes**: permiten delegar una parte del trabajo a otro agente especializado que trabaja por separado y devuelve solo el resultado.
- **Commands**: atajos que disparan directamente un comportamiento específico sin describirlo en lenguaje natural.
- **MCPs**: conectan Claude Code con sistemas externos a la computadora, como el correo, un calendario o una base de datos.

### Links

- Funcionamiento de Claude Code: [How Claude Code works](https://code.claude.com/docs/en/how-claude-code-works)

- Referencia a modelos: [Model configuration](https://code.claude.com/docs/en/model-config)

- Referencia a tools: [Tools reference](https://code.claude.com/docs/en/tools-reference)

- Claude Code Settings: [Settings](https://code.claude.com/docs/en/settings)
