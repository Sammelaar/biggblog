---
title:  Getting Started with Docker – Install & Run Your First Container 🐳⚡
date: 2025-03-28
category: 
summary: 
description: The moment your dev setup stops being messy
author: Sammelaar
cover:
  image: /images/cover_docker.png
alt: 
caption: 
relative: true
showtoc: true
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
# Getting Started with Docker – Install & Run Your First Container 🐳⚡  
*AKA: The moment your dev setup stops being messy*

So you’ve heard about Docker. Maybe you read my last post and now you’re pumped to try it out (if not, check out [What is Docker?](https://blog.innocloud.io/posts/what-is-docker-and-why-should-you-use-it-/) — it’s a good one 👀).  
Today, we’re not just talking about Docker — we’re gonna **use it**.

By the end of this post, you’ll have Docker installed, your first container running, and the confidence to start experimenting like a pro.

Let’s goooo! 🚀

---
## 🧠 What You’ll Learn
- How to install Docker on Windows, macOS, or Linux
- How to verify that Docker is working
- How to run your first container with a single command
- A few cool commands to get you comfy with Docker
---
## Step 1: Install Docker 🧰
Let’s get Docker on your machine. The setup is super simple.

### 🪟 Windows / 🍎 macOS:
1. Go to [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Download Docker Desktop for your OS
3. Install it like any normal app
4. Launch it — you’ll see a little 🐳 whale icon in your system tray or menu bar. That’s Docker saying hello!

> ⚠️ Make sure virtualization is enabled in your BIOS (on some machines) and WSL2 is installed for Windows.
---
### 🐧 Linux (Ubuntu/Debian-style):

Open a terminal and run:

```bash
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

Optional (but handy): Run Docker without `sudo`:

```bash
sudo usermod -aG docker $USER
```

Then log out and back in. You're good to go!

---
## Step 2: Check That Docker Works ✅
Open your terminal and type:

```bash
docker --version
```

You should see something like:

```bash
Docker version 24.0.5, build abcdef1234
```

Nice! Now let’s **run our first container** 🎉

---
## Step 3: Run the Famous "Hello, World" Container 🌍🐳
Type this:

```bash
docker run hello-world
```

Docker will:
- Pull the `hello-world` image from Docker Hub (if you don’t have it yet)
- Spin up a container using that image
- Print out a success message

You’ll see:
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

**YESSS.** It’s alive 🔥

---
## 🛠 Bonus: Useful Docker Commands

Here are a few starter commands to get you comfortable:

| Command                        | What It Does                              |
|-------------------------------|--------------------------------------------|
| `docker ps`                   | Show running containers 🏃                |
| `docker ps -a`                | Show all containers, even stopped ones 🧟 |
| `docker images`               | List all your downloaded images 🗂️        |
| `docker rm <container_id>`    | Delete a container 🗑️                     |
| `docker rmi <image_id>`       | Delete an image 🧼                        |

---
## What Just Happened? 🧠
When you ran `docker run hello-world`, Docker:
- Looked for the image locally
- Pulled it from the cloud if you didn’t have it
- Created a container
- Executed the app inside
- Printed a beautiful success message 💌

You didn’t install dependencies.
You didn’t touch your system Python.
You didn’t cry.

**Docker just worked.**

---

## 🚀 What’s Next?

Now that you’ve run a container, let’s build one of your own!

Coming up next:
**🛠️ Your First Docker App – Build & Run a Container from Scratch**  
We’ll write a simple app, create a Dockerfile, and run it like a boss.

> Got questions or stuck on setup? Drop a comment or reach out — I love helping devs get their first container up and running 🧑‍💻💬
