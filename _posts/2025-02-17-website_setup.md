---
title: "Building a Personal Website with Jekyll, Chirpy, and GitHub Pages"
description: >-
  A comprehensive guide to setting up, customizing, and deploying a Jekyll-based personal website using the Chirpy theme, GitHub Pages, and GitHub Actions.
author: Federico Bellisardi
date: 2025-02-17 18:30:00 +0100
categories: [Blogging, Tutorial]
tags: [jekyll, github_pages, chirpy, website_building]
pin: true
---

# **Building a Personal Website with Jekyll, Chirpy, and GitHub Pages**

This guide explains how to build, configure, and deploy a **personal website** using **Jekyll, Chirpy Theme, GitHub Pages, and GitHub Actions**.

---

## **1️⃣ Prerequisites**
Before you start, ensure you have the following installed:

### **System Requirements**
- **Operating System**: Linux/macOS/Windows
- **Ruby** (>=3.1) and Bundler
- **Jekyll** (static site generator)
- **Git** (for version control)
- **GitHub account** (for hosting with GitHub Pages)
- **Text Editor**: VS Code, Sublime Text, or Nano

### **Install Dependencies (Linux/macOS)**
```sh
sudo apt-get update && sudo apt-get install -y ruby-full build-essential zlib1g-dev
# or for macOS:
brew install ruby
```

### **Install Jekyll and Bundler**
```sh
gem install jekyll bundler
```

---

## **2️⃣ Fork and Clone the Chirpy Theme**
Since we're using the **Chirpy Jekyll Theme**, fork it from GitHub and clone it locally:

```sh
git clone https://github.com/cotes2020/jekyll-theme-chirpy.git my-website
cd my-website
```

Remove the original git history and start fresh:
```sh
rm -rf .git
```

Then, initialize a new repository:
```sh
git init
```

### **Optional: Create a New Branch for Development**
```sh
git checkout -b develop
```

---

## **3️⃣ Install and Run Jekyll Locally**
After cloning, install dependencies:
```sh
bundle install
```

Then, build and serve your site:
```sh
bundle exec jekyll serve
bundle exec htmlproofer ./_site --disable-external

```

Visit **http://127.0.0.1:4000/** to preview your site.

---

## **4️⃣ Customize `_config.yml`**
Open `_config.yml` and update site settings:

```yaml
title: "TITLE"
description: "DESCRIPTION"
baseurl: ""
url: "https://URL.github.io"
remote_theme: cotes2020/jekyll-theme-chirpy
```

### **Create Pages**
Add `about.md` inside the `pages/` directory:
```md
---
layout: page
title: "About Me"
permalink: /about/
---

# About Me

This is Federico Bellisardi's website.
```

Commit changes:
```sh
git add .
git commit -m "chore: customize site config"
```

---

## **5️⃣ Deploy with GitHub Pages**
### **Enable GitHub Pages**
1. **Create a new GitHub repository**: `REPO.github.io`
2. Push your local code:
   ```sh
   git remote add origin https://github.com/REPO/REPO.github.io.git
   git branch -M main
   git push -u origin main
   ```
3. **Go to**: GitHub → Settings → Pages
4. Under **"Build and Deployment"**, select **GitHub Actions**

---

## **6️⃣ Set Up GitHub Actions for Auto Deployment**
Create a GitHub Actions workflow to **auto-build and deploy** Jekyll:

```sh
mkdir -p .github/workflows
nano .github/workflows/pages-deploy.yml
```

Paste the following:
```yaml
name: Deploy Jekyll Site

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
          bundler-cache: true

      - name: Install Jekyll Dependencies
        run: bundle install

      - name: Build Jekyll Site
        run: bundle exec jekyll build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site
```

Commit and push:
```sh
git add .github/workflows/pages-deploy.yml
git commit -m "ci: add GitHub Actions for Jekyll deployment"
git push origin main
```

Now, GitHub will **automatically build and deploy your site** whenever you push changes.

---

## **7️⃣ Additional Customizations**
- **Enable Google Analytics**: Add tracking ID in `_config.yml`
- **Customize CSS**: Modify `_sass/custom.scss`
- **Optimize SEO**: Add `title`, `description`, `keywords` in `_config.yml`

---

## **🚀 Final Steps**
Your Jekyll website is now fully **built, customized, and deployed**!

✔ **Built with Jekyll + Chirpy Theme**  
✔ **Customized `_config.yml`, sidebar, and pages**  
✔ **Auto-deployed via GitHub Actions**  
✔ **Accessible at:** `https://REPO.github.io`

Now, simply **commit and push updates**, and GitHub Pages will rebuild your site automatically!

Enjoy your new personal website! 🚀

