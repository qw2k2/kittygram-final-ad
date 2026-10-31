# Kittygram backend

This directory contains the Django REST API used by the Kittygram application.

The backend provides:
- Token-based user authentication through Djoser and Django REST Framework
- CRUD endpoints for cat profiles
- Achievement management
- Cat photo upload and image URL serialization
- PostgreSQL persistence in the Docker Compose setup

For the full architecture, Docker Compose instructions, CI/CD workflow, and environment configuration, see the [main project README](../README.md).

## Run the backend independently

From this directory, create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
```

Linux / macOS:
```bash
source .venv/bin/activate
```

Windows PowerShell:
```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies and provide a development secret key:

```bash
pip install -r requirements.txt
```

Linux / macOS:
```bash
export SECRET_KEY="local-development-secret"
python manage.py migrate
python manage.py runserver
```

Windows PowerShell:
```powershell
$env:SECRET_KEY = "local-development-secret"
python manage.py migrate
python manage.py runserver
```

The standalone backend uses SQLite when no PostgreSQL environment variables are configured. The Docker Compose setup uses PostgreSQL.
