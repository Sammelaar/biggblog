---
title: Setting Up Pangolin on a VPS – A Reverse Proxy Adventure 🦔🚀 
date: 2025-04-08
category: 
summary: 
description: 
author: Sammelaar
cover:
  image: /images/cover_pangolin.png
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
  - pangolin
  - vps
  - hostinger
  - reverse proxy
  - wireguard
  - docker
  - github
---

*One domain, one VPS, total control.*

I recently decided to set up a rock-solid reverse proxy solution on my VPS, and after testing a few options, I found something *awesome* — **Pangolin** 🦔. It’s simple, powerful, and feels like it was built for people like us who love control without endless config files.

In this post, I’ll walk you through **exactly** how I installed and configured Pangolin on my VPS (hosted via Hostinger), got Docker containers behind it, used **Gerbil** for VPN, secured it with **CrowdSec**, and even added a remote **Newt** agent to route traffic from my homelab. Let's goooo 💻🔧🌍

---

## 🧠 What You'll Learn

- How to install Pangolin with VPN + Docker
- How to tunnel remote traffic with Newt    
- How to set up secure HTTPS with **Let’s Encrypt**
- How to fine-tune **TLS settings** for better security
- How to monitor access and trigger alerts for threats

---

## 🔧 Step 1: Set Up Your VPS
I started by creating a new VPS through my **Hostinger** dashboard — super quick setup.

Once my VPS was running and I SSH’d in, I was ready to install Pangolin.

---

## 🦔 Step 2: Install Pangolin
This was smooth. Just grabbed the installer with `wget` and executed it:

```bash
wget -O installer "<https://github.com/fosrl/pangolin/releases/download/1.1.0/installer_linux_$(uname -m | sed 's/x86_64/amd64/;s/aarch64/arm64/')"
chmod +x ./installer
sudo ./installer
```

During the install:
- Entered my **domain name + email**
- Chose **Gerbil** 🐹 for the VPN engine
- Created admin credentials    
- Accepted default settings for email/invites

Pangolin was now live at:  

👉 `https://pangolin.my-domain.com` ✅

---

## 🐳 Step 3: Install Docker + Set Up Containers
With Pangolin installed, I needed Docker for my container services.

Here’s the full install script I used:

```bash
apt update
apt install -y ca-certificates curl gnupg lsb-release

mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release && echo "$ID")/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/$(. /etc/os-release && echo "$ID") \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

apt update
apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Boom — Docker and Docker Compose installed. ✅

---

## 🛡 Step 4: Harden with CrowdSec
To secure the reverse proxy from brute-force bots and other nonsense, I installed **CrowdSec**. It works seamlessly with Pangolin and adds a smart firewall layer based on community-powered threat intel.

Plus, it supports bouncers like `crowdsec-firewall-bouncer`, `Traefik-bouncer`, or even Slack/Telegram for alerts 📲

Installation is fast, and Pangolin supports it out of the box — just follow the [CrowdSec + Pangolin guide](https://docs.fossorial.io/Pangolin/overview#modular-design).

---

## 🏠 Step 5: Create a Site for My Homelab
Inside the Pangolin dashboard (now live at `https://pangolin.my-domain.com`), I created a new site called **Homelab** — this is where I forward all my remote services like:

- Proxmox
- Portainer    
- Home Assistant
- Anything with a web UI

---

## 🌐 Step 6: Newt Config – Secure Traffic from My Homelab
I used **Newt**, Pangolin’s remote connector, to tunnel traffic from my Proxmox LXC container through to Pangolin on the VPS.

### 🧾 `docker-compose.yml` (on the LXC)

```yaml
services:
  newt:
    image: fosrl/newt
    container_name: newt
    restart: unless-stopped
    environment:
      - PANGOLIN_ENDPOINT=https://pangolin.hostname.com
      - NEWT_ID=your_newt_id
      - NEWT_SECRET=your_newt_secret
```

You get the `NEWT_ID` and `NEWT_SECRET` from the Pangolin dashboard when you add a new connector under “Endpoints”.

---

## 🧱 Step 7: LXC Container Setup in Proxmox
Newt needs Docker inside the container, so I updated the LXC config like this:

```bash
# Required for Docker
features: keyctl=1,nesting=1

# Optional but helpful
lxc.apparmor.profile: unconfined
lxc.cgroup.devices.allow: a
lxc.cap.drop:
```

Then restarted the container and installed Docker using the same script from earlier.

---

## 🔐 Step 8: Let’s Encrypt + Custom TLS Settings
Out of the box, Pangolin handles **Let’s Encrypt SSL** — which is amazing. But I like having control, so I tweaked some TLS settings.

### ✅ My TLS setup:
- TLS 1.2 and 1.3 only
- Removed insecure ciphers
- HSTS and OCSP enabled
- Auto-renew enabled

### 📍You can tweak these under:
`/etc/pangolin/conf/pangolin.yaml` → TLS section:

```yaml CopyEdit

`tls:   minVersion: VersionTLS12   preferServerCipherSuites: true   cipherSuites:     - TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384     - TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305   hsts: true   ocspStapling: true`
```

Don’t forget to restart Pangolin after changes:

```bash CopyEdit

`sudo systemctl restart pangolin`
```

Now my entire Pangolin instance and every site routed through it is 100% HTTPS with hardened TLS 🔐✅

---

## 🚨 Step 9: Monitoring & Alerts
Monitoring self-hosted apps is a must. Here’s what I set up:

### 🔍 Logs & Access:

- Use Pangolin’s built-in dashboard for request logs 
- Integrate **CrowdSec** for attack detection + banning
- Enable JSON logging to export to Grafana/Loki if you want full observability

### 📡 External Monitoring:

- [NetBird](https://www.netbird.io/) – Mesh VPN for remote access + identity-based security
- [Uptime Kuma](https://github.com/louislam/uptime-kuma) – Self-hosted status page
- Telegram bot or Gotify for push alerts

You can even have CrowdSec notify you via Slack or Discord when it bans an IP — amazing visibility into your traffic 🔥

---

## ✅ Final Stack Recap
|Component|Purpose|
|---|---|
|**Pangolin** 🦔|Reverse proxy with VPN support|
|**Docker** 🐳|Container orchestration|
|**Gerbil** 🐹|VPN engine for tunnels|
|**CrowdSec** 🛡|Security + threat mitigation|
|**Newt** 🐍|Secure tunnel from homelab|
|**Let’s Encrypt** 🔐|Auto TLS + certs|
|**Uptime Kuma / NetBird** 🔍|Monitoring & alerts|

The result? A clean, secure, auto-updating reverse proxy that connects my remote containers and self-hosted services like a dream.

---