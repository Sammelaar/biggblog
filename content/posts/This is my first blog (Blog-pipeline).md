---
title: "This is my first blog (Blog-pipeline)"
date: 2024-12-31
catergory:
summary:
description:
author: "Sammie"
tags:
  - tech
  - obsidian
  - hugo
  - github
  - hosting
---

## <u>The goal</u>
- To build a blog about cool things that are passing by in my life. Such things as tech or gadgets I bought/used.
- 
## <u>How does this blog works?</u>
My blog is build with the following tools/products:
- **Obsidian**
	- Obsidian is a powerful note-taking tool that focuses on building a personal knowledge base using Markdown files. It allows users to create a network of interconnected notes through links and tags, making it easy to organize and retrieve information. \n Go download it yourself! [https://obsidian.md/](https://obsidian.md/)
- **Hugo**
	- Hugo is a fast and flexible static site generator designed for building websites. It uses templates and markdown files to create content, making it easy to structure and organize. With its lightning-fast build times, Hugo is particularly well-suited for developers and content creators who need to generate static sites quickly and efficiently. \n Go download it yourself! [https://gohugo.io](https://gohugo.io)
- **Custom scripts**
	- By custom scripts the local markdown files from Obsidian will be copied to the local Hugo-site.
- **GitHub**
	- GitHub is a web-based platform for version control and collaboration, primarily used by developers to manage and share code. It leverages Git, a distributed version control system, to track changes to code over time, enabling multiple people to work on the same project simultaneously. \n Go use it yourself! [https://github.com](https://github.com)
- **TransIP-hosting**
	- TransIP is a Dutch hosting provider offering a wide range of web hosting services, including domain registration, cloud hosting, virtual private servers (VPS), and dedicated servers. Known for its reliable infrastructure and high-performance servers, TransIP allows users to easily manage their websites and online projects through an intuitive control panel.

## <u>So, how do you build this?</u>

#### Obsidian

- First we start creating a folder called _posts_ in Obsidian where you can store all your blogposts.
!![Image Description](/images/Pasted%20image%2020250103220213.png)

```
```

hugo new site Biggelaar.it --format yaml

## Generate an SSH key (Mac/Linux/Windows)

ssh-keygen -t rsa -b 4096 -C "sam@biggelaar.it"

