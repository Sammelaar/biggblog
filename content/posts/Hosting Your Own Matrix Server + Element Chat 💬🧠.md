---
title: Hosting Your Own Matrix Server + Element Chat 💬🧠 
date: 2025-04-22
category: 
summary: 
description: 
author: Sammelaar
cover:
  image: /images/cover_matrix.png
alt: 
caption: 
relative: true
showtoc: true
searchHidden: false
toc: false
draft: false
disableShare: true
ShowReadingTime: true
ShowCodeCopyButtons: true
tags:
  - tech
  - docker
  - github
---
*Because you deserve private, encrypted, decentralized communication.*

---
Ever wanted your own chat platform — one that’s **secure**, **open**, **decentralized**, and **completely self-hosted**?

Welcome to **Matrix**.

Matrix is a protocol for real-time communication, built to be federated (like email) and encrypted by default. And on top of Matrix, there’s **Element** — a slick, modern chat client that makes using your server feel like Slack meets Signal.

In this guide, I’ll walk you through how to **spin up your own Matrix homeserver (Synapse)** and host **Element web** so you can start chatting from your domain, with your rules.

---

## 🧠 What You'll Learn
- What Matrix and Element are (and why they're awesome)
- How to deploy a Matrix Synapse server with Docker
- How to host Element web and point it to your homeserver
- How to secure it with a reverse proxy + HTTPS
- Tips for inviting users, mobile apps, and federation

---

## 🔍 What is Matrix?
Matrix is a protocol — not just an app — for secure, decentralized messaging.

- Fully open-source
- End-to-end encrypted
- Works across servers (federated like email)
- Supports voice, video, file sharing, bots, and bridges (IRC, Slack, Discord, Telegram…)

Your Matrix identity might look like this:
```
@you:yourdomain.com
```

---

## 🛠️ What is Element?
[Element](https://element.io/) is the main Matrix client — open source, beautiful, and super customizable. You can run it locally, in your browser, or host your own copy of the web app.

Together, Matrix + Element = Your own encrypted chat platform. 🧑‍💻

---

## 🚀 Step-by-Step: Install Matrix Synapse Server
We’ll install [**Synapse**](https://github.com/matrix-org/synapse), the most popular Matrix server implementation.

### ✅ Requirements:
- VPS or homelab machine (Ubuntu 22.04 or similar)
- Docker + Docker Compose
- A domain name (e.g., `chat.yourdomain.com`)
- A reverse proxy (we’ll use Traefik or Nginx)

---

### 📁 Folder Structure
```bash
mkdir -p ~/matrix/synapse
cd ~/matrix/synapse
```

### 🧾 Create `.env` file
```env
SERVER_NAME=yourdomain.com
POSTGRES_PASSWORD=supersecurepassword
```

---

### 🐳 `docker-compose.yml`
```yaml
version: "3.7"

services:
  synapse:
    image: matrixdotorg/synapse:latest
    container_name: synapse
    restart: unless-stopped
    environment:
      - SYNAPSE_SERVER_NAME=${SERVER_NAME}
      - SYNAPSE_REPORT_STATS=yes
      - SYNAPSE_CONFIG_PATH=/data/homeserver.yaml
    volumes:
      - ./data:/data
    depends_on:
      - postgres
    networks:
      - matrix

  postgres:
    image: postgres:13
    restart: unless-stopped
    environment:
      POSTGRES_DB=synapse
      POSTGRES_USER=synapse
      POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
    volumes:
      - ./postgres:/var/lib/postgresql/data
    networks:
      - matrix

networks:
  matrix:
    driver: bridge
```

---

## 🔐 Step 2: Setup Reverse Proxy with HTTPS

### Option A: With Traefik (recommended)
Just add labels to your `synapse` container, like:
```yaml
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.matrix.rule=Host(`matrix.yourdomain.com`)"
  - "traefik.http.routers.matrix.entrypoints=websecure"
  - "traefik.http.routers.matrix.tls.certresolver=letsencrypt"
```

### Option B: With Nginx
Install Certbot and create a basic proxy config:

```nginx
server {
  server_name matrix.yourdomain.com;

  location / {
    proxy_pass http://localhost:8008;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $remote_addr;
  }

  listen 443 ssl;
  ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
}
```

---

## ✅ Step 3: Run Synapse
```bash
docker compose up -d
```

Then initialize your first user:

```bash
docker exec -it synapse register_new_matrix_user -c /data/homeserver.yaml http://localhost:8008
```

You’ll be asked to enter a username, password, and optionally make this account an admin.

Congrats! Your Matrix server is online 💬🧠

---

## 🖼 Step 4: Deploy Element Web
Create another folder: `~/matrix/element`

### `docker-compose.yml` for Element:
```yaml
version: "3"

services:
  element:
    image: vectorim/element-web:latest
    container_name: element
    restart: unless-stopped
    volumes:
      - ./config.json:/app/config.json
    ports:
      - "8080:80"
```

### `config.json`
```json
{
  "default_server_config": {
    "m.homeserver": {
      "base_url": "https://matrix.yourdomain.com",
      "server_name": "yourdomain.com"
    }
  },
  "disable_custom_urls": true,
  "default_theme": "light",
  "brand": "MyMatrix",
  "features": {
    "feature_pinning": true
  }
}
```

Then start it:

```bash
docker compose up -d
```

Point your browser to `https://element.yourdomain.com` and log in with your Matrix username!

---
## 📱 Bonus: Use on Mobile
You can use your Matrix server with the **Element app** on iOS or Android!

- Download [Element](https://element.io/get-started)
- Tap *"Other server"*
- Enter `https://matrix.yourdomain.com`
- Log in!

---

## 🔒 Optional: Enable Federation
Want your Matrix server to talk to other Matrix servers (like `matrix.org`)? You'll need to:

- Make sure port 8448 is open
- Add a `server_name` DNS SRV record (optional but helpful)
- Set up well-known file under `/.well-known/matrix/server`

More info: [Matrix Federation Guide](https://matrix-org.github.io/synapse/latest/federate.html)

---

## 🧠 Why Host Your Own Matrix Server?
- ✅ Fully encrypted messaging
- ✅ Federated: you control your domain and users
- ✅ Bridge with Slack, Discord, Telegram, etc.
- ✅ Beautiful UI via Element
- ✅ Open source, community driven

---

**That’s it!** You now have your own chat server, powered by Matrix and Element — hosted under your domain, fully encrypted, and ready for friends, family, or your whole team.