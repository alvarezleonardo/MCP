# MCP Chat (punto de partida)

Aplicación de línea de comandos que habilita un chat interactivo con un modelo de lenguaje (vía la API de Anthropic) y le suma herramientas, recursos y prompts a través de un servidor **MCP (Model Context Protocol)**.

Esta es la **versión base** del Módulo 1: trae los mismos archivos que la solución pero con **TODOs para completar** mientras seguís las notas. La solución de referencia está en [`../cli_project_COMPLETE`](../cli_project_COMPLETE/).

> Teoría paso a paso en las notas del módulo: [Qué es MCP](../01-que-es-mcp.md) · [Arquitectura](../02-arquitectura-y-flujo.md) · [Herramientas](../03-herramientas-e-inspector.md) · [Cliente](../04-cliente-mcp.md) · [Recursos](../05-recursos.md) · [Prompts](../06-prompts.md).

## Requisitos

- Python 3.10+
- API key de Anthropic (los ejemplos usan Claude como implementación concreta; ver la sección [Independiente del modelo](../../README.md#independiente-del-modelo-model-agnostic) del README raíz).

## Configuración

Creá un archivo `.env` en la raíz del proyecto con tu credencial:

```
ANTHROPIC_API_KEY=""   # tu clave secreta de Anthropic
```

## Instalación

Con [uv](https://docs.astral.sh/uv/) (recomendado):

```bash
uv sync
```

## Cómo correr

```bash
# Aplicación CLI de chat completa
uv run main.py

# Inspector de MCP en el navegador (probar el servidor sin la CLI)
uv run mcp dev mcp_server.py
```

## El ejercicio

Para completar la funcionalidad MCP:

1. Resolvé los TODOs en `mcp_server.py` (definir tools, recursos y prompts).
2. Implementá las funciones faltantes en `mcp_client.py` (`list_tools`, `call_tool`, `read_resource`, etc.).

Compará tu avance contra la [solución completa](../cli_project_COMPLETE/) cuando lo necesites.

## Uso

### Chat básico

Escribí tu mensaje y presioná Enter para conversar con el modelo.

### Recuperación de documentos (recursos)

```
> Contame sobre @deposition.md
```

### Comandos (prompts)

Usá `/` para ejecutar prompts del servidor MCP (autocompletan con Tab):

```
> /summarize deposition.md
```
