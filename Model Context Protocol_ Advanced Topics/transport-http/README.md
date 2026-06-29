# Servidor MCP sobre StreamableHTTP

Demostración del transporte **StreamableHTTP** del Model Context Protocol: a diferencia de STDIO (que exige cliente y servidor en la misma máquina), este transporte expone el servidor MCP **por HTTP**, habilitando servidores remotos a los que un cliente puede conectarse por red.

> Teoría: [06 — Transporte StreamableHTTP](../06-streamable-http.md) y [04 — Tipos de mensajes JSON](../04-mensajes-json.md).

## Qué demuestra

- El servidor (`main.py`) corre sobre StreamableHTTP en lugar de STDIO.
- `index.html` es un cliente web mínimo para interactuar con el servidor desde el navegador.
- Permite observar el modelo de conexiones (handshake con `mcp-session-id`, SSE) descrito en las notas.

## Requisitos

- Python 3.10+

## Instalación

```bash
uv sync
```

## Cómo correr

Levantá el servidor MCP:

```bash
uv run main.py
```

Con el servidor corriendo, abrí `index.html` en el navegador para usar el cliente web.

## Estructura

| Archivo | Rol |
|---------|-----|
| `main.py` | Servidor MCP sobre StreamableHTTP |
| `index.html` | Cliente web mínimo para probarlo desde el navegador |
