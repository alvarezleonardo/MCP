# Demo de sampling (MCP)

Demostración de **sampling** en el Model Context Protocol: el **servidor le pide al cliente** que llame a un modelo de lenguaje en su nombre, en lugar de integrarse directo con la API del modelo. Así, el cliente (que ya tiene la conexión y las credenciales) paga el uso de tokens y el servidor queda simple y sin API keys.

> Teoría: [01 — Sampling (muestreo)](../01-sampling.md).

## Qué demuestra

- El servidor (`server.py`) define una tool que, en vez de llamar al modelo, emite una solicitud de sampling con `ctx.session.create_message(...)`.
- El cliente (`client.py`) atiende esa solicitud con una `sampling_callback` que llama al modelo (vía el SDK de Anthropic) y devuelve el texto generado.

## Requisitos

- Python 3.10+
- API key de Anthropic, ya que es el **cliente** quien llama al modelo (los ejemplos usan Claude; ver [Independiente del modelo](../../README.md#independiente-del-modelo-model-agnostic)).

## Configuración

Asegurate de tener la variable de entorno `ANTHROPIC_API_KEY` seteada con una clave válida (en tu entorno o en un `.env`):

```
ANTHROPIC_API_KEY=""   # tu clave secreta de Anthropic
```

## Instalación

```bash
uv sync
```

## Cómo correr

El cliente levanta el servidor como subproceso vía STDIO:

```bash
uv run client.py
```

## Estructura

| Archivo | Rol |
|---------|-----|
| `server.py` | Servidor MCP con la tool que emite la solicitud de sampling |
| `client.py` | Cliente MCP con la `sampling_callback` que llama al modelo |
