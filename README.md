# Kittygram

Kittygram is a full-stack web application for sharing cats. Users can create accounts, publish cat profiles with photos, colors and achievements, and browse the community catalogue.

## Features

- User registration, token-based authentication, and logout
- Create, view, edit, and delete cat profiles
- Upload cat photos
- Store a cat's name, birth year, and color
- Attach achievements to cats
- Browse a paginated cat catalogue
- Manage data through a Django REST API
- Serve the React frontend and API through an Nginx gateway

## Tech stack

**Backend**
- Python 3.9
- Django 3.2
- Django REST Framework
- Djoser and DRF Token Authentication
- PostgreSQL
- Gunicorn

**Frontend**
- React 17
- React Router
- Create React App

**Infrastructure**
- Docker and Docker Compose
- PostgreSQL 13
- Nginx
- GitHub Actions

## Architecture

The application is split into three main services:

- **Frontend** — React single-page application for registration, authentication, and cat profile management
- **Backend** — Django REST API for users, cats, and achievements
- **Gateway** — Nginx serves the built frontend and proxies API, admin, and media requests to the backend

PostgreSQL stores application data. Docker Compose coordinates the services and persistent volumes.

## Run locally with Docker Compose

### Requirements

- Git
- Docker Engine
- Docker Compose plugin

### 1. Clone the repository

```bash
git clone https://github.com/qw2k2/kittygram-final-ad.git
cd kittygram-final-ad
```

### 2. Configure environment variables

Create a local `.env` file from the example:

**Linux / macOS**
```bash
cp .env.example .env
```

**Windows PowerShell**
```powershell
Copy-Item .env.example .env
```

Edit `.env` before starting the services. Set a unique, randomly generated `SECRET_KEY` and a strong `POSTGRES_PASSWORD`. The values in `.env.example` are placeholders for local development only.

### 3. Build and start the application

```bash
docker compose up --build
```

Open the application at [http://localhost:9000](http://localhost:9000).

To stop the services:

```bash
docker compose down
```

To stop the services and remove the local database volume as well:

```bash
docker compose down -v
```

The last command permanently deletes the local PostgreSQL data volume.

## Running tests

### Backend

The backend tests use Django's test runner. From the repository root:

**Linux / macOS**
```bash
cd backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export SECRET_KEY="local-test-secret"
python manage.py test
```

**Windows PowerShell**
```powershell
cd backend
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:SECRET_KEY = "local-test-secret"
python manage.py test
```

### Frontend

From the repository root:

```bash
cd frontend
npm ci
npm test -- --watchAll=false
```

## Continuous integration

The GitHub Actions workflow in `.github/workflows/kittygram_workflow.yml` runs on pushes and pull requests targeting `main`. It:

1. Installs backend dependencies and runs Django tests.
2. Installs frontend dependencies and runs the React test suite.

The workflow uses a temporary CI-only Django secret and does not require deployment credentials. Automated deployment is not currently enabled by this workflow.

## Project status

This is an educational full-stack project demonstrating a React frontend, Django REST API, containerized services, and automated testing. The repository includes starter tests; test coverage and production hardening can be expanded further.
