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

Secrets (DB passwords, admin mail/password) are set in `docker-compose.yml` for local dev only — use placeholders in docs; never commit real credentials. For production, use a `.env` file and variable substitution.

## Access

| What        | URL                      |
|------------|---------------------------|
| **FrontOffice (shop)** | http://localhost:8080      |
| **BackOffice (admin)** | http://localhost:8080/admin-dev |
| **phpMyAdmin**         | http://localhost:8081      |

**Back Office login (after a fresh install):**  
Email: `admin@prestashop.local` · Password: `prestashop`  
(Set in `docker-compose.yml` via `ADMIN_MAIL` / `ADMIN_PASSWD`; only applied when PrestaShop installs. Change after first login; do not use in production.)

If you get "The employee does not exist, or the password provided is incorrect", try the image default password **`prestashop_demo`** with the same email, or use **Forgot your password?** on the login page. For a clean slate: `docker compose down -v` then `docker compose up -d` (this deletes all PrestaShop data and reinstalls with the credentials above).

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

## Module expirydate (install via Git clone)

Install the expiry-date module **via Git clone** (PRD 2.4):

```bash
# From presta-site directory
git clone <URL_OF_ps-module-expiry-date_REPO> modules/expirydate
docker compose down && docker compose up -d
```

Then in **BO → Modules → Module Manager**: search **"Date d'expiration"**, click **Install**. The `modules/expirydate` folder is bind-mounted so the container sees it.

## Theme (Task 10)

The child theme **NutriSport Hummingbird** is in `themes/nutrisport-hummingbird/`. It is mounted into the container so the Back Office can see it.

1. After the first install, go to **Design > Theme & Logo**.
2. Select **NutriSport Hummingbird Child** and save.
3. If the theme has no preview image, copy `preview.png` from the Hummingbird theme (inside the container: `themes/hummingbird/preview.png`) into `themes/nutrisport-hummingbird/` on the host.
