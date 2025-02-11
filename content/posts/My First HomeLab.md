---
title: My First HomeLab
date: 2025-02-11
category: HomeLab
summary: 
description: 
author: Sammelaar
cover:
  image: "/images/my_first_homelab.png"
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
  - homelab
  - docker
  - github
  - proxmox
---
## <u> Introduction </u> :speech_balloon:
After my [first blog](https://blog.biggelaar.it/posts/this-is-my-first-blog-blog-pipeline/) about building this blog, I started thinking: what’s next? 🤔  

Should I focus on software again, or is it time to switch things up and dive into hardware? Then, an idea struck me—why not build my very own little data center? So, for February, I’m going to build my HomeLab! 🌟🚀

## <u> Infrastructure: Building the Foundation of My HomeLab :toolbox:</u> 
Every great system starts with a solid foundation, and in the world of HomeLabs, that foundation is **infrastructure**. Before diving into complex configurations, self-hosted services, or automation, it's crucial to design a reliable and scalable setup that meets your needs.

In this chapter, I’ll walk you through the key components of my HomeLab infrastructure—**from hardware choices to networking, virtualisation, and storage solutions**. Whether you’re just starting out or refining an existing setup, I’ll share insights, lessons learned, and best practices to help you build a robust and efficient HomeLab environment.

So, let’s get started by exploring the backbone of every HomeLab: it's infrastructure! 🏗️🔧

### Networking: The Backbone of a Reliable HomeLab! :wireless:
Every HomeLab needs a connection to the world wide web so it can communicate with services and so you can use the services you build from 'the outside'. But what do you need for that? Well you'll need a solid network infrastructure. 

With all types of IT, you can make this as complex as you would like. I chose to make it easy and secure. Don't make your own HomeLab to complex, if you want to change something you need to understand your own building! :wink:

For my LAN, I chose Ubiquiti Unifi to work with. Unifi is a brand that has a solid fundament, not that complex, easy to maintain and has standard build in security. For wireless I have Aruba access points. :wireless:

#### How does my configuration looks like?

### Virtualisation vs. Containerisation: Choosing the Right Approach for Your HomeLab. :desktop_computer:
When setting up a HomeLab, one of the biggest decisions is how to deploy and manage your workloads. Should you run full virtual machines (VMs), leverage lightweight containers, or use a mix of both?

**Virtualisation** provides isolation and flexibility, making it ideal for running multiple operating systems on a single host. Meanwhile, **containerisation** offers efficiency and speed, allowing for rapid deployment and scaling of applications with minimal overhead.

In this chapter, I’ll break down the key differences between virtualisation and containerisation, explore their pros and cons, and share how I use them in my HomeLab setup. Whether you’re looking to optimize resource usage, improve security, or experiment with new technologies, understanding these two approaches is essential for building a powerful and efficient HomeLab.

Let’s dive in! 🚀

#### Hypervisor

#### Docker 

#####  Docker with VS code and GitHub

gh auth login

echo YOUR_GITHUB_PERSONAL_ACCESS_TOKEN | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin



docker build -t ghcr.io/YOUR_GITHUB_USERNAME/YOUR_IMAGE_NAME:latest .

docker push ghcr.io/YOUR_GITHUB_USERNAME/YOUR_IMAGE_NAME:latest

example: docker push ghcr.io/johndoe/myapp:latest

docker pull ghcr.io/YOUR_GITHUB_USERNAME/YOUR_IMAGE_NAME:latest
docker run -d -p 8080:80 ghcr.io/YOUR_GITHUB_USERNAME/YOUR_IMAGE_NAME
