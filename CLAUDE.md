# Contexto del proyecto

Usuario: Luis Soto. Trabaja desde un iPad, en sesiones de Claude Code en la nube. Responder en español.

## Qué hay en este repositorio
- `.claude/skills/`: skills de diseño y animación de Emil Kowalski (`npx skills add emilkowalski/skill`). Versiones en `skills-lock.json`.
- `.claude/skills/find-skills/`: busca skills nuevas (`npx skills add vercel-labs/skills -s find-skills`).
- Al instalar skills, hacerlo en el proyecto (`-a claude-code --copy`, sin `-g`) y subirlas a GitHub: la máquina en la nube se borra y lo global se pierde.
- `.mcp.json`: servidores MCP del proyecto.
  - `perplexity`: necesita la variable `PERPLEXITY_API_KEY` en el entorno de la nube.
  - `playwright`: navegador sin interfaz que usa el Chromium preinstalado (`/opt/pw-browsers/chromium`).

## Conectores que Luis activa en claude.ai
Firecrawl, PostHog y Composio (este último como conector personalizado). Se cargan al empezar una sesión nueva.

## Proyecto pendiente: web «A literatura en Pelamios»
- Biblioteca de la Rúa dos Pelamios, 28 · 15705 Santiago de Compostela. Textos en gallego.
- Ya existe una versión hecha por Luis: `index.html` con la carpeta `assets/` al lado. Siete idiomas, cuatro colores y un apartado propio para cada opción del menú.
- Totales esperados: 1.582 ejemplares en papel (inventario de Lucas, repetidos incluidos), 154 libros digitales («Luis Dixital»), 1.736 en total; 137 ejemplares repetidos («Repetidos»: 65 títulos, 72 ejemplares de más); 1.643 títulos distintos.
- Entrega: un zip con `index.html` en la raíz, para subir al servidor de Gulans (acepta cualquier tipo de archivo).
- No inventar datos del catálogo: trabajar solo con los archivos que envíe Luis.
