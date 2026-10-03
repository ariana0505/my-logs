# Skills y MCPs para el proyecto

---

## Objetivos de la clase 🎯

---

## Skills

Una skill es una herramienta que nos permite agregar conocimiento a Claude para realizar ciertas tareas que no están en su base de conocimientos o queremos que se haga de cierta manera.

Dependiendo del scope (`~/.claude` o `.claude`), estas se instalan bajo el folder `/skills/<skill-name>/SKILL.md`.

Las skills soportan nested directories, o sea que puedes tener skills por folder, no solo a nivel proyecto.

Para instalar skills el método recomendado es usando el comando `npx skills`.

> 💡 **Dato curioso:** *Discoverable* significa que una skill puede ser encontrada y usada automáticamente por Claude sin invocarla manualmente. Claude lee la `description` del `SKILL.md` de cada skill como parte de su contexto inicial, y si tu petición coincide con esa descripción, la activa solo (sin necesidad de escribir `/nombre-skill`). Por eso es importante que la `description` esté bien redactada.

### Estructura de una skill

Una skill (`my-skill`) se compone de:

- **`SKILL.md`** — archivo principal con la descripción y las instrucciones de la skill.
- **`references`** — carpeta con documentación o referencias adicionales.
- **`scripts`** — carpeta con scripts que la skill puede ejecutar.
- **`assets`** — carpeta con archivos/recursos que la skill puede usar (plantillas, imágenes, etc.).

### Skills para frontend (ayuda para repo Albumcito Facilito)

```
npx skills add vercel-labs/next-skills --skill next-best-practices
npx skills add vercel-labs/agent-skills --skill react-best-practices
```

### Skills para backend (ayuda para repo Albumcito Facilito)

```
npx skills add Kadajett/agent-nestjs-skills
```

### Nuestra skill para testing (ayuda para repo Albumcito Facilito)

Para crear nuestra propia skill vamos a necesitar instalar un plugin de Anthropic que contiene una skill llamada `skill-creator`:

```
/plugin marketplace add anthropics/skills
```

Dividiremos esto en 2 prompts:

1. "Add tests libraries for frontend project and backend project to do BDD testing using Gherkin"
2. "Create a skill called bdd-gherkin, this skill should indicate how create testing for nextjs applications and nestjs apis"

---

## ¿Qué es un MCP?

Un MCP (**Model Context Protocol**) es un protocolo abierto que permite conectar a Claude con herramientas y fuentes de datos externas (APIs, bases de datos, servicios, etc.), para que pueda leer información o ejecutar acciones fuera de su base de conocimiento, más allá de lo que puede hacer con skills o comandos.

A diferencia de una skill (que agrega *conocimiento* o instrucciones), un MCP agrega *capacidades*: le da a Claude herramientas nuevas (funciones) que puede invocar en tiempo real, como consultar Notion, Slack, una base de datos, GitHub, etc.

### MCP de Playwright (ayuda para repo Albumcito Facilito)

Playwright se ha vuelto el estándar para test E2E, pero por el momento lo usaremos para hacer un review de las features que desarrollamos directamente en el browser.

```
claude mcp add playwright npx @playwright/mcp@latest
```

---

## Let's prompt (ayuda para repo Albumcito Facilito)

Prompt de ejemplo que combina todo lo anterior (skills de frontend, backend, testing y el MCP de Playwright):

> "Create a feature to allow view a set of albums in the home page and when i click on some album show the cody stickers.
>
> In frontend application use skills next-best-practices and react-best-practices
>
> For backend project use skills agent-nestjs-skills
>
> Create tests for boths using skill bdd-gherkin
>
> Review changes using playwright mcp"
