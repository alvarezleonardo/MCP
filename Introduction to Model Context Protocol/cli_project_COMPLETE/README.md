# MCP Chat (solución completa)

Aplicación de línea de comandos que habilita un chat interactivo con un modelo de lenguaje (vía la API de Anthropic) y le suma herramientas, recursos y prompts a través de un servidor **MCP (Model Context Protocol)**.

Esta es la **solución de referencia** del Módulo 1: el servidor de gestión documental y el cliente MCP completamente implementados. Si querés hacer el ejercicio desde cero, usá [`../cli_project`](../cli_project/), que trae los mismos archivos con TODOs para completar.

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

## Uso

### Chat básico

Escribí tu mensaje y presioná Enter para conversar con el modelo.

### Recuperación de documentos (recursos)

Usá `@` seguido del ID de un documento para incluir su contenido en la consulta:

```
> Contame sobre @deposition.md
```

### Comandos (prompts)

Usá el prefijo `/` para ejecutar prompts definidos en el servidor MCP (autocompletan con Tab):

```
> /summarize deposition.md
```

## Estructura

| Archivo | Rol |
|---------|-----|
| `mcp_server.py` | Servidor MCP: define tools (`read_doc_contents`, `edit_document`), recursos y prompts |
| `mcp_client.py` | Cliente MCP: `list_tools`, `call_tool`, `read_resource`, `list_prompts`, `get_prompt` |
| `main.py` | Punto de entrada de la CLI |
| `core/` | Lógica de la app: chat, integración con el modelo, CLI y orquestación de tools |

### Agregar documentos

Editá el diccionario `docs` en `mcp_server.py`.

> Nota: `core/` es prácticamente idéntico al de [`../cli_project`](../cli_project/); lo que cambia entre la base y la solución es el contenido de `mcp_server.py` y `mcp_client.py`.
