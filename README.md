# Arcane Docker Deployment

This repository contains the Docker Compose configuration and environment templates to deploy **Arcane**, a web-based manager designed to control and monitor containerized infrastructures.

Project-Link:  https://getarcane.app/
        

## 🚀 Prerequisites

Before deploying, ensure your system has the following installed:
* **Docker** (Engine v20.10+ recommended)
* **Docker Compose** (V2 plugin)

The repository includes pre-configured tracking folders (`arcane/projects`, `arcane/builds`, and `arcane/backups`) containing `.gitkeep` files. When you clone this repository, these folders will automatically belong to your local user, preventing any Docker permission issues.

## 🛠️ Setup & Deployment

Follow these steps to get your instance up and running:

### 1. Clone and Configure Environment
Clone this repository to your server, copy the environment template, and open it for editing:
```bash
cp .env.example .env
nano .env
```

### 2. Generate an Encryption Key
Arcane requires a secure 32-byte hex key to encrypt sensitive internal data. Generate one using `openssl` and paste it into the `ARCANE_ENCRYPTION_KEY` variable inside your `.env` file:
```bash
openssl rand -hex 32
```

### 3. Update Database Secrets
Change the default values for `DB_NAME`, `DB_USER`, and `DB_PASSWORD` inside the `.env` file to ensure your database layer is secure.

### 4. Start the Application
Launch the containers in detached (background) mode:
```bash
docker compose up -d
```

## 🌐 Access & Monitoring

* **Web Interface:** Open your browser and navigate to `http://<your-server-ip>:3552` (or `http://localhost:3552` if running locally).
* **Logs:** To view live logs from the Arcane manager and database, run:
  ```bash
  docker compose logs -f
  ```
* **Status:** Check container health states using:
  ```bash
  docker compose ps
  ```

## 🛡️ Security Note

The `.env` file contains highly sensitive production credentials and encryption keys. It is explicitly ignored via `.gitignore` and **must never** be committed to public version control systems.
