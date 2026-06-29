# MCP Chat con acceso al sistema de archivos (roots)

Aplicación de línea de comandos que habilita un chat interactivo con un modelo de lenguaje (vía la API de Anthropic) y le suma, a través de un servidor **MCP (Model Context Protocol)**, acceso **controlado** al sistema de archivos mediante **roots**, además de una tool de conversión de video.

> Teoría: [03 — Roots (raíces)](../03-roots.md).

## Requisitos

- Python 3.10+
- API key de Anthropic (los ejemplos usan Claude; ver [Independiente del modelo](../../README.md#independiente-del-modelo-model-agnostic)).
- FFmpeg (para la conversión de video).

## Configuración

Primero instalá FFmpeg (necesario para convertir videos). En macOS:

```bash
brew install ffmpeg
```

### Variables de entorno

Copiá `.env.example` a `.env` y completá tus valores:

```bash
cp .env.example .env
```

```
CLAUDE_MODEL="claude-sonnet-4-0"   # o el modelo de Claude que prefieras
ANTHROPIC_API_KEY=""               # tu clave secreta de Anthropic
```

## Instalación

Con [uv](https://docs.astral.sh/uv/):

```bash
uv sync
```

## Cómo correr

Al iniciar el proyecto debés indicar uno o más **directorios raíz (roots)** a los que el servidor MCP tendrá acceso. Solo se podrán leer archivos y carpetas **dentro** de esos roots:

```bash
uv run main.py <root1> [root2] [root3] ...
```

Ejemplos:

```bash
# Un directorio
uv run main.py /ruta/a/videos

# Varios directorios
uv run main.py /home/user/videos /mnt/storage/media ~/Documentos

# Directorio actual
uv run main.py .
```

## Características

### Acceso controlado al sistema de archivos

El servidor solo puede acceder a archivos y carpetas dentro de los roots indicados. Esto aporta seguridad al limitar el acceso a ubicaciones aprobadas.

### Tools disponibles

- **list_roots**: lista los directorios raíz accesibles.
- **read_dir**: lee el contenido de un directorio (debe estar dentro de un root).
- **convert_video**: convierte videos MP4 a otros formatos (avi, mov, webm, mkv, gif).

### Conversión de video

La tool de conversión usa FFmpeg para pasar archivos MP4 a varios formatos:

- Formatos estándar: AVI, MOV, WebM, MKV.
- Conversión a GIF con ajustes optimizados.
- Preset de calidad media para equilibrar tamaño y calidad.

## Estructura

| Archivo | Rol |
|---------|-----|
| `mcp_server.py` | Servidor MCP: tools de filesystem (con chequeo de roots) y conversión de video |
| `mcp_client.py` | Cliente MCP |
| `main.py` | Punto de entrada de la CLI (recibe los roots como argumentos) |
| `core/` | Lógica de la app: chat, integración con el modelo, CLI y conversión de video |
