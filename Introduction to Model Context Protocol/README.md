# Módulo 1 — Introducción a MCP

Fundamentos del **Model Context Protocol**: qué problema resuelve, cómo está armado y cómo construir, paso a paso, un servidor y un cliente MCP completos usando el SDK oficial de Python.

Al terminar este módulo vas a entender las **tres primitivas** de un servidor MCP —herramientas, recursos y prompts— y quién controla cada una.

## Ruta de lectura

| # | Nota | Qué cubre |
|---|------|-----------|
| 01 | [Qué es MCP](./01-que-es-mcp.md) | El problema de integración y cómo MCP lo resuelve |
| 02 | [Arquitectura y flujo](./02-arquitectura-y-flujo.md) | Host, cliente, servidor, transporte y el flujo completo de una consulta |
| 03 | [Herramientas e Inspector](./03-herramientas-e-inspector.md) | `FastMCP`, definir tools con decoradores, probar con el Inspector |
| 04 | [Cliente MCP](./04-cliente-mcp.md) | `list_tools()` y `call_tool()`, manejo de sesión |
| 05 | [Recursos](./05-recursos.md) | Recursos directos y con plantilla, `@menciones` |
| 06 | [Prompts](./06-prompts.md) | Indicaciones reutilizables, comandos `/slash` |
| 07 | [Repaso de primitivas](./07-primitivas-mcp.md) | Tools vs recursos vs prompts: quién controla cada una |

## Proyectos

| Carpeta | Para qué |
|---------|----------|
| [`cli_project/`](./cli_project/) | Punto de partida con TODOs para completar mientras seguís las notas |
| [`cli_project_COMPLETE/`](./cli_project_COMPLETE/) | Solución completa de referencia |

Ambos implementan un **servidor de gestión documental** (leer/editar documentos en memoria) y una **CLI de chat** que conversa con el modelo usando ese servidor.

### Cómo correr

```bash
cd cli_project_COMPLETE
uv sync
uv run mcp dev mcp_server.py   # Inspector en el navegador
uv run main.py                 # CLI de chat completa
```

Necesitás un `.env` con tu `ANTHROPIC_API_KEY` (ver el README raíz del repo).
