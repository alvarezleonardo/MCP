# Demo de logging y notificaciones de progreso (MCP)

Demostración del **Model Context Protocol** sobre transporte **STDIO**, enfocada en los mensajes que el **servidor envía al cliente** durante la ejecución de una tool: logs (`context.info`) y progreso (`context.report_progress`).

> Teoría: [02 — Logging y notificaciones de progreso](../02-logging-y-progreso.md) y [05 — Transporte STDIO](../05-transporte-stdio.md).

## Qué demuestra

- El servidor (`server.py`) expone una tool que emite mensajes de log y reportes de progreso mientras trabaja.
- El cliente (`client.py`) registra una `logging_callback` (a nivel sesión) y una `progress_callback` (por llamada) para mostrar ese feedback en la terminal.

No requiere API key: es comunicación servidor-cliente pura, sin llamadas a un modelo.

## Requisitos

- Python 3.10+

## Instalación

```bash
uv sync
```

## Cómo correr

El cliente levanta el servidor como subproceso vía STDIO:

```bash
uv run client.py
```

Vas a ver en la terminal los mensajes de log y el avance de progreso a medida que la tool se ejecuta.

## Estructura

| Archivo | Rol |
|---------|-----|
| `server.py` | Servidor MCP con la tool que emite logs y progreso |
| `client.py` | Cliente MCP con las callbacks de logging y progreso |
