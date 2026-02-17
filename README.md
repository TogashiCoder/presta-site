# presta-site – NutriSport PrestaShop

PrestaShop site for NutriSport (FR, IT, BE). This repo is meant to be run via Docker.

## Prerequisites

- **Docker** and **Docker Compose** (v2)
- Git

No local PHP or MySQL required when using Docker.

## Installation

### 1. Clone the repo

```bash
git clone https://github.com/TogashiCoder/presta-site.git
cd presta-site
```

### 2. Start the stack

```bash
docker compose up -d
```

Wait a few minutes on first run (PrestaShop installs automatically). Then open the URLs below.

### 3. (Optional) Environment

Secrets (DB passwords, etc.) are set in `docker-compose.yml` for local dev only. For production, use a `.env` file and variable substitution .
## Access

| What        | URL                      |
|------------|---------------------------|
| **FrontOffice (shop)** | http://localhost:8080      |
| **BackOffice (admin)** | http://localhost:8080/admin-dev |
| **phpMyAdmin**         | http://localhost:8081      |

Default BackOffice credentials (local dev): with auto-install the image may use a default admin password (e.g. check PrestaShop Docker image docs). Change after first login. Do not use production credentials here.

## Useful commands

```bash
# Start
docker compose up -d

# Stop
docker compose down

# View logs
docker compose logs -f prestashop

# Shell inside PrestaShop container
docker exec -it prestashop /bin/bash

# Clear PrestaShop cache (from host)
docker exec -it prestashop rm -rf /var/www/html/var/cache/*

# Enable a module (inside container)
docker exec -it prestashop php bin/console prestashop:module enable <module_name>

# Disable a module
docker exec -it prestashop php bin/console prestashop:module disable <module_name>
```

## Ports

- **8080** – PrestaShop (HTTP)
- **8081** – phpMyAdmin
- **3307** – MariaDB (host); use only if connecting from host (e.g. `127.0.0.1:3307`)

## Docker services

- **prestashop** – PrestaShop (Apache + PHP)
- **prestashop-db** – MariaDB 10.6
- **prestashop-phpmyadmin** – phpMyAdmin (optional)

Data is persisted in Docker volumes `presta-data` and `presta-db-data`.
