---
title: Install Traefik with Docker Compose – The Secure Dev-Friendly Reverse Proxy 🛡️🔐🚪  
date: 2025-04-03
category: 
summary: 
description: 
author: Sammelaar
cover:
  image: /images/cover_traefik.png
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
*Secure all your Docker services with auto-magic HTTPS*

So you’ve been playing with Docker and Docker Compose. You’ve spun up Portainer, maybe a Flask app, maybe even a database. Everything works great — until you realize:

> “Wait… I have 5 apps and they all want to use port 80 or 443 😅”

Enter **Traefik** — the magical, self-configuring reverse proxy for Docker.  
You define a few labels, let it read your Docker socket, and BOOM — instant routing, SSL, dashboards, load balancing… all in real-time. 🤯

Let’s walk through how to install **Traefik in Docker Compose**, use it to route traffic to containers like Portainer — without ever touching `nginx.conf` and secure it by HTTPS with a certificate.

Thanks to **Let’s Encrypt** and Traefik’s built-in TLS support, it’s easier than ever. Let’s upgrade your setup and make your apps production-worthy 🔒🚀

---

## 🧠 What You’ll Learn

- What Traefik is and why it rocks 🤘
- How to install it using Docker Compose
- How to expose services like Portainer through Traefik
- A simple example using Docker labels
- How to enable HTTPS in Traefik with Let’s Encrypt  
- How to use `docker-compose` with separate files for Traefik and Portainer  
- How to set up secure routing with TLS and valid SSL certs  
- How to test it locally with a self-signed wildcard domain

---
## 🤔 What is Traefik?
Traefik is a modern reverse proxy and load balancer built specifically for microservices and container setups. It **monitors your Docker environment**, watches for labels on containers, and automatically routes traffic to them based on rules you define.

### In plain English:
- You give your app a label like: `traefik.http.routers.myapp.rule=Host(`myapp.local`)`
- Traefik goes: “Got it! Routing traffic for myapp.local to this container!”
- You didn’t write any config files. It just works. 😍

## 💡 How It Works
- Traefik reads labels from your containers via the Docker socket
- It creates a router based on `Host()` rules
- The entrypoint `web` listens on port 80
- The dashboard is enabled at `localhost:8080`
- Only services with `traefik.enable=true` are exposed 🔒

## 🧪 Folder Structure
Same clean layout:

```
docker/
├── traefik/
│   ├── docker-compose.yml
│   ├── traefik.yml
│   └── acme.json  (auto-generated cert storage)
├── portainer/
│   └── docker-compose.yml
```

---

## ⚙️ Step 1: Updated Traefik Config with HTTPS

### 📄 `traefik/docker-compose.yml`

```yaml
version: "3.8"

services:
  traefik:
    image: traefik:v2.10
    container_name: traefik
    command:
      - "--providers.file.filename=/etc/traefik/traefik.yml"
    ports:
      - "80:80"
      - "443:443"
      - "8080:8080"
    volumes:
      - ./traefik.yml:/etc/traefik/traefik.yml:ro
      - ./acme.json:/acme.json
      - /var/run/docker.sock:/var/run/docker.sock:ro
    networks:
      - traefik

networks:
  traefik:
    name: traefik
```

⚠️ **Important:**  
Before starting Traefik, create the `acme.json` file and lock down the permissions:

```bash
touch acme.json
chmod 600 acme.json
```

---

### 🧾 `traefik/traefik.yml`

```yaml
entryPoints:
  web:
    address: ":80"
  websecure:
    address: ":443"

providers:
  docker:
    exposedByDefault: false
  file:
    filename: /etc/traefik/traefik.yml

certificatesResolvers:
  letsencrypt:
    acme:
      email: your-email@example.com
      storage: /acme.json
      httpChallenge:
        entryPoint: web

api:
  dashboard: true
  insecure: true  # Remove in production!
```

🔐 This config:
- Sets up two entry points: HTTP (`web`) and HTTPS (`websecure`)
- Enables the Let’s Encrypt resolver called `letsencrypt`
- Uses the HTTP challenge (port 80) for cert verification

---

## 🛠 Step 2: Secure Portainer with HTTPS
### 📄 `portainer/docker-compose.yml`

```yaml
version: "3.8"

services:
  portainer:
    image: portainer/portainer-ce
    container_name: portainer
    restart: always
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.portainer.rule=Host(`portainer.example.com`)"
      - "traefik.http.routers.portainer.entrypoints=websecure"
      - "traefik.http.routers.portainer.tls.certresolver=letsencrypt"
      - "traefik.http.services.portainer.loadbalancer.server.port=9000"
    volumes:
      - portainer_data:/data
    networks:
      - traefik

volumes:
  portainer_data:

networks:
  traefik:
    external: true
```

✅ This setup tells Traefik:
- Only expose Portainer over HTTPS (via `websecure`)
- Use the `letsencrypt` resolver to get a valid SSL certificate

---

## 🔄 Step 3: Run Everything
Start Traefik:

```bash
cd docker/traefik
docker compose up -d
```

Start Portainer:

```bash
cd ../portainer
docker compose up -d
```

🎉 Traefik will request an SSL cert for `portainer.example.com` — **automatically** — and serve your app over HTTPS.

---

## 🧪 Test It Out
Make sure DNS for `portainer.example.com` points to your server (you can test with a custom domain or local DNS override like [nip.io](https://nip.io)).

Then go to:

👉 [https://portainer.example.com](https://portainer.example.com)  
👉 [http://localhost:8080](http://localhost:8080) — Traefik dashboard

✅ You should see a valid certificate issued by Let’s Encrypt.

---

## 🛡 Pro Tips
- Use wildcard DNS services like `*.nip.io`, `sslip.io`, or local DNS for dev  
- Don’t use `localhost` for HTTPS testing — Let’s Encrypt won’t issue certs for it  
- Use `docker compose logs -f traefik` to debug cert issues  
- Avoid exposing `--api.insecure=true` in production

---

## 🚀 What’s Next?
You’ve now got a **fully modular**, **secure**, and **scalable** reverse proxy stack with:
- 🔄 Automatic SSL
- 🧩 Service separation
- 🔐 Production-ready HTTPS
---