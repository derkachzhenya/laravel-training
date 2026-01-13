# Laravel Training Project

A personal Laravel training project created to practice backend development, clean architecture, and modern Laravel features.

---

## 🎯 Purpose
This project is designed to improve practical Laravel skills through hands-on development and real-world scenarios.

The main goals include:
- Understanding Laravel core concepts
- Writing clean, maintainable code
- Following best practices and conventions
- Gaining confidence with Git and GitHub workflows

---

## 🚀 Features
- MVC architecture
- CRUD operations
- Authentication & authorization
- Database migrations & seeders
- Eloquent ORM
- Validation & form requests
- RESTful API (in progress)
- Error handling & logging

---

## 🛠 Tech Stack
- **Laravel**
- **PHP**
- **MySQL**
- **Git & GitHub**

---

## 📂 Local Project Setup

```bash
git clone https://github.com/derkachzhenya/laravel-training.git
cd laravel-training

composer install
cp .env.example .env
php artisan key:generate

php artisan migrate
php artisan serve
```

---

## 🐳 Docker Deployment (Server Quick Start)

These steps match the working setup used on a Ubuntu server (e.g., DigitalOcean).

### 1) Install Docker + Compose (Ubuntu)

```bash
apt update
apt install -y ca-certificates curl gnupg

install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" \
  > /etc/apt/sources.list.d/docker.list

apt update
apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
service docker start
```

### 2) Clone the project

```bash
cd /var/www
git clone https://github.com/derkachzhenya/laravel-training.git laravel-training
cd laravel-training
```

### 3) Create and edit `.env`

```bash
cp .env.example .env
nano .env
```

Minimal `.env` values for Docker:

```env
APP_ENV=production
APP_DEBUG=false
APP_URL=http://<SERVER_IP_OR_DOMAIN>

DB_HOST=db
DB_DATABASE=myapp
DB_USERNAME=myapp
DB_PASSWORD=myapp_pass

CACHE_STORE=file
SESSION_DRIVER=file
QUEUE_CONNECTION=sync
```

### 4) Fix permissions for the container user

```bash
chown -R 1000:1000 /var/www/laravel-training
```

### 5) Expose a port in `docker-compose.yml`

For public access:

```yaml
ports:
  - "8081:80"
```

For local-only access on the server:

```yaml
ports:
  - "127.0.0.1:8081:80"
```

### 6) Build and start containers

```bash
docker compose up -d --build
```

### 7) Prepare Laravel inside the container

```bash
docker compose exec app git config --global --add safe.directory /var/www/html
docker compose exec app composer install --no-dev --optimize-autoloader
docker compose exec app php artisan key:generate
docker compose exec app php artisan migrate --force
docker compose exec app php artisan config:cache
```

### 8) Verify

```bash
curl -I http://127.0.0.1:8081
```

In a browser:

```
http://<SERVER_IP>:8081
```
