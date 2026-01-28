# Instrucciones de instalación

Breve guía para instalar las dependencias Python y Node del proyecto.

## Python

- Crear y activar un entorno virtual (recomendado):

  PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

  CMD:

```cmd
python -m venv .venv
.venv\Scripts\activate.bat
```

- Instalar dependencias desde `requirements.txt`:

```bash
pip install -r requirements.txt
```

## Node.js

- Instalar dependencias del proyecto (usa `package.json`):

```bash
npm install
```

- Opcional: instalar la herramienta global solicitada:

```bash
npm install -g dkmaker-mcp-rest-api
```

- Opcional: corregir vulnerabilidades detectadas:

```bash
npm audit fix
```

## Archivos relevantes

- [requirements.txt](requirements.txt) — dependencias Python
- [package.json](package.json) — dependencias Node

## Notas

- Requiere Python 3.8+ y Node.js 14+.
- En Windows, si falla la instalación global, ejecuta la terminal como administrador.
