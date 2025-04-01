---
title: This is my first blog! 🔥🚀
date: 2025-01-17
category: 
summary: 
description: 
author: Sammelaar
cover:
  image: /images/cover/cover_blogpipeline.png
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
  - obsidian
  - hugo
  - github
  - hosting
---
# This is my first blog! 🔥🚀
Last November, NetworkChuck dropped an [inspiring video](https://youtu.be/dnE7c0ELEH8?si=0KOi9RjaDTtLycFK) that got my gears turning. :bulb: Fast forward to 2025, and I’ve set myself an epic challenge: every month this year, I’m diving into something new in the world of IT.

For January, I’m kicking things off by following Chuck’s video step by step, and I can’t wait to share what I learn. Stay tuned, because each month, a fresh blog post will drop with my latest tech adventures. Let’s make 2025 a year of leveling up together! :rocket: :man_student:

## The Goal :round_pushpin:
My goal is to create a semi-automated workflow that transforms a note from Obsidian into a webpage for a website, with version control and tracking managed through GitHub.
![Image Description](/images/blog_pipeline.png)
## How does this blog works? :man_shrugging:
My blog is built with the following tools:

- **Obsidian**
	- Obsidian is a powerful note-taking tool that focuses on building a personal knowledge base using Markdown files. It allows users to create a network of interconnected notes through links and tags, making it easy to organize and retrieve information. \n Download it here! [https://obsidian.md/](https://obsidian.md/)
- **Hugo**
    - Hugo is a fast and flexible static site generator designed for building websites. It uses templates and Markdown files to create content, making it easy to structure and organize. With its lightning-fast build times, Hugo is particularly well-suited for developers and content creators who need to generate static sites quickly and efficiently. Download it here! [https://gohugo.io](https://gohugo.io/)
- **Custom scripts**
    - Custom scripts copy local Markdown files from Obsidian will be copied to the local Hugo-site.
- **GitHub**
    - GitHub is a web-based platform for version control and collaboration, primarily used by developers to manage and share code. It leverages Git, a distributed version control system, to track changes to code over time, enabling multiple people to work on the same project simultaneously. Download it here! [https://github.com](https://github.com/)
- **TransIP-hosting**
    - TransIP is a Dutch hosting provider offering a wide range of web hosting services, including domain registration, cloud hosting, virtual private servers (VPS), and dedicated servers. Known for its reliable infrastructure and high-performance servers, TransIP allows users to easily manage their websites and online projects through an intuitive control panel.

## So, how do you build this? :memo:
### Setting up Obsidian

- First, create a folder called _posts_ in Obsidian where you can store all your blogposts.
- Start writing your first blog post now! :fire:
### Setting up Hugo

- Install Git from [GitHub.com](https://github.com/git-guides/install-git)
- Install Go from [Go.dev](https://go.dev/dl/)
- Install Hugo from [Gohugo.io](https://gohugo.io/)
### Create a new site in Hugo

```bash

## Verify Hugo works

hugo version

## Create a new site

hugo new site websitename
cd websitename
```
### Find your favorite Hugo-theme

- Go have a look at [Themes.gohugo.io/](https://themes.gohugo.io/)!
	- Every theme has instructions on how to use it.
    - When you have your theme, add this as a Git submodule:
	    - A **Git submodule** is a feature in Git that allows you to include one Git repository as a subdirectory within another Git repository. It helps manage dependencies or related projects that are developed independently but need to be included in your main project.

```bash
## Initialize a git repository (Make sure you are in your Hugo website directory)

git init

## Set global username and email parameters for git

git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

## Install a theme (we are installing the Terminal theme here). Once downloaded it should be in your Hugo themes folder

## Find a theme ---> <https://themes.gohugo.io/>

git submodule add --depth=1 <https://github.com/adityatelange/hugo-PaperMod.git> themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)

```
### Personalize your theme

- Most of the themes you can download do have an example configuration-file that you can use. Try this one to test if Hugo is working.
- I put the example file from the PaperMod-theme below so you can use this one.
- To edit this hugo.yaml file you can use a tool as Visual Studio Code or the following command in Terminal **nano hugo.yaml** or in PowerShell **notepad hugo.yaml**.

```
baseURL: "<https://examplesite.com/>"
title: ExampleSite
paginate: 5
theme: PaperMod

enableRobotsTXT: true
buildDrafts: false
buildFuture: false
buildExpired: false

googleAnalytics: UA-123-45

minify:
  disableXML: true
  minifyOutput: true

params:
  env: production # to enable google analytics, opengraph, twitter-cards and schema.
  title: ExampleSite
  description: "ExampleSite description"
  keywords: [Blog, Portfolio, PaperMod]
  author: Me
  # author: ["Me", "You"] # multiple authors
  images: ["<link or path of image for opengraph, twitter-cards>"]
  DateFormat: "January 2, 2006"
  defaultTheme: auto # dark, light
  disableThemeToggle: false

  ShowReadingTime: true
  ShowShareButtons: true
  ShowPostNavLinks: true
  ShowBreadCrumbs: true
  ShowCodeCopyButtons: false
  ShowWordCount: true
  ShowRssButtonInSectionTermList: true
  UseHugoToc: true
  disableSpecial1stPost: false
  disableScrollToTop: false
  comments: false
  hidemeta: false
  hideSummary: false
  showtoc: false
  tocopen: false

  assets:
    # disableHLJS: true # to disable highlight.js
    # disableFingerprinting: true
    favicon: "<link / abs url>"
    favicon16x16: "<link / abs url>"
    favicon32x32: "<link / abs url>"
    apple_touch_icon: "<link / abs url>"
    safari_pinned_tab: "<link / abs url>"

  label:
    text: "Home"
    icon: /apple-touch-icon.png
    iconHeight: 35

  # profile-mode
  profileMode:
    enabled: false # needs to be explicitly set
    title: ExampleSite
    subtitle: "This is subtitle"
    imageUrl: "<img location>"
    imageWidth: 120
    imageHeight: 120
    imageTitle: my image
    buttons:
      - name: Posts
        url: posts
      - name: Tags
        url: tags

  # home-info mode
  homeInfoParams:
    Title: "Hi there \\U0001F44B"
    Content: Welcome to my blog

  socialIcons:
    - name: x
      url: "<https://x.com/>"
    - name: stackoverflow
      url: "<https://stackoverflow.com>"
    - name: github
      url: "<https://github.com/>"

  analytics:
    google:
      SiteVerificationTag: "XYZabc"
    bing:
      SiteVerificationTag: "XYZabc"
    yandex:
      SiteVerificationTag: "XYZabc"

  cover:
    hidden: true # hide everywhere but not in structured data
    hiddenInList: true # hide on list pages and home
    hiddenInSingle: true # hide on single page

  editPost:
    URL: "<https://github.com/><path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link

  # for search
  # <https://fusejs.io/api/options.html>
  fuseOpts:
    isCaseSensitive: false
    shouldSort: true
    location: 0
    distance: 1000
    threshold: 0.4
    minMatchCharLength: 0
    limit: 10 # refer: <https://www.fusejs.io/api/methods.html#search>
    keys: ["title", "permalink", "summary", "content"]
menu:
  main:
    - identifier: categories
      name: categories
      url: /categories/
      weight: 10
    - identifier: tags
      name: tags
      url: /tags/
      weight: 20
    - identifier: example
      name: example.org
      url: <https://example.org>
      weight: 30
# Read: <https://github.com/adityatelange/hugo-PaperMod/wiki/FAQs#using-hugos-syntax-highlighter-chroma>
pygmentsUseClasses: true
markup:
  highlight:
    noClasses: false
    # anchorLineNos: true
    # codeFences: true
    # guessSyntax: true
    # lineNos: true
    # style: monokai

```
### Copying your Markdown file to your Hugo-site.

- So, we have build our post in Obsidian? :white_check_mark:
- We set up Hugo? :white_check_mark:

Let’s publish the post to our site then! :slightly_smiling_face:

To publish your post, you’ll need to copy your .md-file to the posts-folder in the Hugo-folder. Let me help, use the following code:
### Windows :window:

```powershell
robocopy sourcepath destination path /mir
```
### Mac/Linux :penguin:

```bash
rsync -av --delete "sourcepath" "destinationpath"
```

Don’t forget to add a title and other attributes:

```markdown
---
title: This is my first blog!
date:
description:
author: Me
showtoc: true
toc: false
draft: false
ShowReadingTime: false
ShowCodeCopyButtons: true
tags:  - tag1  
			 - tag2
---
```

Now your are good to go! :dash:
### Finally, testing!

```bash
## Verify Hugo works with your theme by running this command

hugo server -t themename
```

When used the command go to: localhost:1313 in your browser and have a look. :eyes:
### Missing your images? :framed_picture:

You worked hard, wrote a lot of text, used a lot of images and then… :boom: no images, just test.png… No worries! Again, let me help your with a script to copy the images to the right folder in your Hugo-structure.
### Windows :window:

```powershell
import os
import re
import shutil

# Paths (using raw strings to handle Windows backslashes correctly)
posts_dir = r"posts-folder"
attachments_dir = r"images-folder"
static_images_dir = r"static-folder Hugo"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)
        
        with open(filepath, "r", encoding="utf-8") as file:
            content = file.read()
        
        # Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)
        
        # Step 3: Replace image links and ensure URLs are correctly formatted
        for image in images:
            # Prepare the Markdown-compatible link with %20 replacing spaces
            markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)
            
            # Step 4: Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)

        # Step 5: Write the updated content back to the markdown file
        with open(filepath, "w", encoding="utf-8") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")
```
### Mac/Linux :penguin:

```bash
import os
import re
import shutil

# Paths
posts_dir = "posts-folder"
attachments_dir = "images-folder"
static_images_dir = "static-folder Hugo"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)
        
        with open(filepath, "r") as file:
            content = file.read()
        
        # Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)
        
        # Step 3: Replace image links and ensure URLs are correctly formatted
        for image in images:
            # Prepare the Markdown-compatible link with %20 replacing spaces
            markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)
            
            # Step 4: Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)

        # Step 5: Write the updated content back to the markdown file
        with open(filepath, "w") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")
```
## Optional: Save your code to GitHub! :octopus:

### Generate an SSH key (Mac/Linux/Windows) :key:

To make authentication yourself on [Github.com](http://Github.com) via terminal you’ll need to generate a SSH key. Use the following command! :man_technologist:

```bash
## Generate an SSH key (Mac/Linux/Windows)

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
### Create an repository in GitHub and connect to GitHub! :card_index_dividers:

When you're familiar with GitHub you know what to do, but for the people who don’t know just use the green button!
![Image Description](/images/image.png)

It doesn’t matter if you create a public or private repo, just start testing what fits for you! :wink:

![Image Description](/images/image%201.png)

Repo created? Use your SSH key to authenticate with GitHub. :closed_lock_with_key:

```bash
## Show the public key that is needed for GitHub

cat id_rsa.pub
```

Copy the result from the command above and add this as New SSH key into [GitHub.com](http://GitHub.com).
![Image Description](/images/image%202.png)

After you’ve added this SSH key, let’s test if it works! :ballot_box_with_check:

```bash
## Login to GitHub by your SSH key. Check if you're in your .ssh-folder!

ssh -T git@github.com
Enter passphrase for key '/Users/<username>/.ssh/id_rsa': 
Hi Sammelaar! You've successfully authenticated, but GitHub does not provide shell access.
```
### Add your local Git-repo to GitHub! :octopus:

A couple of steps later and then finally, uploading your work to GitHub! :raised_hands:

By using the following commands, you’ll adding your local Git-repo to GitHub:

```bash
## First, add a remote Git-repository.

git remote add origin git@github.com:Username/repository.git

## Be sure your Markdown-files are converted by Hugo!

Hugo

## Add all your files to your Git-repo.

git add . 

## Commit your changes.

git commit -m "This is my first commit!"

## And finally, push!

git push -u origin master
```

Now, check your GitHub-repo! :rocket:
### Deploy your GitHub-repo to your webserver! :computer:

- Wrote your blog?
- Chose your website theme?
- Published your files to GitHub?
- Now, upload it to your webserver! :fire:

First, we need to connect to your webserver. This could be hosted by a provider or locally hosted, in my case it is hosted by a provider. :globe_with_meridians:

To connect you can use a SSH key if you want. :wink:

```bash
## To connect to my webserver, I use

ssh <username>@webserver
```

When connected, we need to make a deployment script. This script will clone your remote GitHub-repo to this webserver and copy your Hugo public-folder to your website-folder. Use nano to create this script-file! :file:
	- **Nano** is a simple and user-friendly text editor for the command line. It is widely used on Unix-like operating systems, including Linux, because of its straightforward interface and ease of use.

```bash
## First, create the file by the following command:

nano deploy.sh

## Then copy the following script and edit the parameters.

#!/bin/bash

REPO_URL="git@github.com:<username>/<GitHub-repo>"
TARGET_FOLDER="<website-folder>"
TEMP_FOLDER="/tmp/<website>"
SPECIFIC_FOLDER="public"

# Remove old temporary folder
rm -rf $TEMP_FOLDER

# Clone the repository
git clone $REPO_URL $TEMP_FOLDER

# Copy the specific folder to the target location
rsync -av --delete $TEMP_FOLDER/$SPECIFIC_FOLDER/ $TARGET_FOLDER/

# Clean up
rm -rf $TEMP_FOLDER

echo "Deployment completed successfully!"
```

### Master Script :wink:
You want to push it all by one script? Here you go! :rocket:

```bash
#!/bin/bash

set -euo pipefail

# Change to the script's directory
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

cd "$SCRIPT_DIR"

# Set variables for Obsidian to Hugo copy
sourcePath="/Users/.../.../posts"
destinationPath="/Users/.../.../content/posts"  

# Set GitHub Repo
myrepo="..."

# Check for required commands
for cmd in git rsync python3 hugo; do
if ! command -v $cmd &> /dev/null; then
echo "$cmd is not installed or not in PATH."
exit 1
fi

done
 
# Step 1: Check if Git is initialized, and initialize if necessary
if [ ! -d ".git" ]; then
echo "Initializing Git repository..."
git init
git remote add origin $myrepo
else
echo "Git repository already initialized."
if ! git remote | grep -q 'origin'; then
echo "Adding remote origin..."
git remote add origin $myrepo
fi
fi

# Step 2: Sync posts from Obsidian to Hugo content folder using rsync
echo "Syncing posts from Obsidian..."
if [ ! -d "$sourcePath" ]; then
echo "Source path does not exist: $sourcePath"
exit 1
fi

if [ ! -d "$destinationPath" ]; then
echo "Destination path does not exist: $destinationPath"
exit 1
fi

rsync -av --delete "$sourcePath" "$destinationPath"

# Step 3: Process Markdown files with Python script to handle image links
echo "Processing image links in Markdown files..."
if [ ! -f "images.py" ]; then
echo "Python script images.py not found."
exit 1
fi

if ! python3 images.py; then
echo "Failed to process image links."
exit 1
fi

# Step 4: Build the Hugo site
echo "Building the Hugo site..."

cd /Users/User/Folder

if [ ! -f "config.toml" ] && [ ! -f "config.yaml" ] && [ ! -f "config.json" ]; then
echo "Error: Hugo config file not found. Did you initialize the Hugo site?"
exit 1
fi

if ! hugo; then
echo "Hugo build failed."
exit 1
fi

# Step 5: Add changes to Git
echo "Staging changes for Git..."

if git diff --quiet && git diff --cached --quiet; then
echo "No changes to stage."
else
git add .
fi

# Step 6: Commit changes with a dynamic message
commit_message="New Blog Post on $(date +'%Y-%m-%d %H:%M:%S')"

if git diff --cached --quiet; then
echo "No changes to commit."
else
echo "Committing changes..."
git commit -m "$commit_message"
fi

# Step 7: Push all changes to the main branch
echo "Deploying to GitHub Main..."
if ! git push origin master; then
echo "Failed to push to main branch."
exit 1
fi

echo "Deploying to TransIP..."
if ! ssh username@server; then
echo "Failed to push to TransIP."
exit 1
fi

# Run deploy.sh on the remote server
echo "Executing deploy.sh on TransIP..."
ssh username@server 'bash -s' < ./deploy.sh

echo "All done! Site synced, processed, committed, built, and deployed."
```

### Here you go, you own blog! :fire:
![Alt text for the image](/images/blog_biggelaar.png)