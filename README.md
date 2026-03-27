# Test Task — DevOps (Effective Mobile)

## 📦 Overview

This project demonstrates a simple web application deployed using **Docker** and **Docker Compose**, with **nginx as a reverse proxy**.

Architecture:

```
User → nginx → backend (FastAPI)
```

* **nginx** handles incoming HTTP requests on port `80`
* **backend** (FastAPI) processes requests internally on port `8080`
* Backend is not exposed to the host and is accessible only внутри docker-сети

---

## 🛠 Tech Stack

* Python 3.13
* FastAPI
* Uvicorn
* nginx (official image)
* Docker & Docker Compose
* uv (dependency manager)

---

## 🚀 How to Run

### 1. Clone repository

```bash
git clone https://github.com/KlyaksaOFF/test_task_devops.git
cd test_task_devops
```

### 2. Build and start containers

```bash
docker compose up --build
```

---

## ✅ How to Check

After containers are running, open:

```
http://localhost
```

or run:

```bash
curl http://localhost
```

Expected response:

```
Hello from Effective Mobile!
```

---

## ⚙️ How It Works

### Backend

* FastAPI application
* Runs on `0.0.0.0:8080`
* Not exposed outside Docker network

### nginx

* Listens on port `80`
* Proxies requests to backend using:

```
http://backend:8080
```

* Configuration is mounted via volume:

```
./nginx/nginx.conf → /etc/nginx/conf.d/default.conf
```

### Docker Compose

* Defines two services:

  * `backend`
  * `nginx`
* Only nginx is exposed to host (`80:80`)
* Services communicate via Docker internal network using service names

---

## 📁 Project Structure

```
backend/
├── Dockerfile
├── app.py

nginx/
└── nginx.conf

docker-compose.yml
pyproject.toml
uv.lock
README.md
```

---

## 🔒 Notes

* Backend service is not accessible from host (by design)
* No hardcoded IP addresses are used
* nginx communicates with backend via service name (`backend`)
* Dependencies are locked using `uv.lock`

---

## ▶️ Stop Containers

```bash
docker compose down
```
