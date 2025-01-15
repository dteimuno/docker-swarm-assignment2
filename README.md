# docker-swarm-assignment2
# Drupal and PostgreSQL Docker Configuration

This `docker-compose.yml` file sets up a Drupal 8.2 environment with a PostgreSQL 14 database. It is designed for local development and uses Docker volumes and secrets for better modularity and security.

## Services

### 1. **Drupal**
- **Image:** `drupal:8.2`
- **Ports:** Exposes port `8080` on the host machine and maps it to port `80` in the container.
- **Volumes:** 
  - `drupal-modules` → `/var/www/html/modules`: Stores Drupal custom/contributed modules.
  - `drupal-profiles` → `/var/www/html/profiles`: Stores Drupal installation profiles.
  - `drupal-sites` → `/var/www/html/sites`: Stores site-specific configurations and files.
  - `drupal-themes` → `/var/www/html/themes`: Stores Drupal themes.

### 2. **PostgreSQL**
- **Image:** `postgres:14`
- **Environment Variables:**
  - `POSTGRES_PASSWORD_FILE`: Points to the secret file containing the PostgreSQL password.
- **Secrets:** Uses an external secret `psql-pw` to securely store the database password.
- **Volumes:**
  - `drupal-data` → `/var/lib/postgresql/data`: Stores PostgreSQL data persistently.

## Volumes
Docker volumes are used to persist data and share files between the host and the containers:
- `drupal-modules`
- `drupal-profiles`
- `drupal-sites`
- `drupal-themes`
- `drupal-data`

## Secrets
An external secret `psql-pw` is required for securely storing the PostgreSQL password. Ensure the secret is created beforehand using Docker secrets management.

## Usage

1. **Ensure Docker is installed** on your system.
2. **Create the external secret** for PostgreSQL password:
   ```bash
   echo "your_secure_password" | docker secret create psql-pw -
3. **Start the services using:**
   ```bash
   docker-compose up -d
   ```
4. **Access Drupal at http://localhost:8080 in your browser.**
