# PenTestBox

PenTestBox is a modular, automated penetration testing toolbox designed for security analysts and red teams. It supports plugin-based orchestration of popular open-source pentest tools, secure storage, audit logging, and automated reporting.

## Features

- Modular, plugin-driven core (auto-discover plugins)
- Full-async workflow (FastAPI + Celery + Redis)
- Command-line interface (CLI) for all operations
- Supports essential pentest tools (see below)
- Secure: RBAC, Fernet encryption for secrets, audit logs
- Reports (HTML, PDF, CSV) with Jinja2 templates
- All artifact storage handled by MinIO (object store)
- PostgreSQL for metadata, audit, user/role management

## MVP Plugins

- [x] `nikto` (Web scanner)
- [x] `gobuster` (Web fuzzer)

Other plugins are scaffolded and ready for rapid implementation.

## Requirements

- Python 3.11+
- Docker + Docker Compose

## Setup

1. **Clone the repo:**

   ```sh
   git clone https://github.com/YOUR_ORG/PenTestBox.git
   cd PenTestBox
   ```

2. **Copy .env example and configure:**

   ```sh
   cp .env.example .env
   # Edit variables as needed (DB, Redis, MinIO)
   ```

3. **Run with Docker Compose:**

   ```sh
   docker compose up --build
   ```

   The API, worker, DB, Redis, and MinIO will all be started.

4. **Install CLI into your local Python environment:**

   ```sh
   poetry install
   poetry run pentestbox-cli --help
   ```

5. **Create admin user via the API or CLI.**

## Usage

1. **Initialize a pentest target:**

   ```sh
   poetry run pentestbox-cli init --target https://example.com
   ```

2. **Run a scan (example with nikto):**

   ```sh
   poetry run pentestbox-cli scan --module nikto --target https://example.com
   ```

3. **Generate a report:**

   ```sh
   poetry run pentestbox-cli report --format pdf --target https://example.com
   ```

## API Documentation

Access Swagger UI at: `http://localhost:8000/docs`

## Security Notes

- All secrets are Fernet-encrypted at rest.
- Full audit trail for all actions.
- RBAC (admin/analyst) enforced for API and CLI.

## License

MIT License. All tools integrated are open-source and redistributable under their respective licenses.

## Project Structure

See below for file/folder organization.