# Push Local Repo to GitHub Reoop Using with gh auth login (github cli)


## What is Git?

Git is a distributed version control system used to track changes in files and manage project history. It keeps a history of changes, so you can manage and experiment with your work without the fear of losing your progress.

## What is Github?
GitHub is a cloud-based platform that acts as a hosting service for Git repositories, allowing developers to store, manage, and collaborate on code projects. It provides version control, enabling multiple people to work on the same codebase simultaneously through tools like pull requests, branching, and issue tracking.

## Why Git?

* Track changes
* Restore old versions
* Collaborate safely
* Use branches
* Manage code professionally

  
## Git vs GitHub

* Git = version control tool
* GitHub = cloud hosting platform for Git repositories


## Preruisite:
* Git installed
* gh cli installed
* VS Code installed
* GitHub account
* Local project folder ready 

## Step 1: Create Empty Repo on GitHub Website
### Go to GitHub and create a new repository.

Choose:
* Repository name: my-devsecops-portfolio
* Public or Private
* Do NOT initialize with README
* Click Create repository

# Step 2: Open Project in VS Code
* Open VS Code
* File → Open Folder
* Select your project

Open terminal:
Ctrl + `

## Step 3: Go to Project Folder

$ cd /mnt/g/WEB_PYTHON/django_proj/portfolio

## Step: 4 Install GitHub CLI (gh)
Option A (recommended for Ubuntu/WSL)
sudo apt update
sudo apt install gh -y
Verify installation:

$ gh --version

gh version 2.45.0 (2025-07-18 Ubuntu 2.45.0-1ubuntu0.3)
https://github.com/cli/cli/releases/tag/v2.45.0

## Step:  5 Login to GitHub using CLI

Run:
$ gh auth login

```bash

You’ll see prompts:

Step-by-step answers:
1. Choose GitHub.com
? What account do you want to log into?
> GitHub.com

2. Choose protocol
? What is your preferred protocol for Git operations?
> HTTPS

(choose HTTPS since you're avoiding SSH issues)

3. Authentication method
? How would you like to authenticate GitHub CLI?
> Login with a web browser

4. Open browser

It will show a code like:

8FGH-1234

👉 Open:
https://github.com/login/device

Paste code
Authorize GitHub CLI

3. Confirm login

Back in terminal:

$ gh auth status

administrator@WIN-RJ32TRRFOFP:/mnt/g/WEB_PYTHON/django_proj/portfolio$ gh auth status
github.com
  ✓ Logged in to github.com account anisur81 (/home/administrator/.config/gh/hosts.yml)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'

```

## Step: 4. Make Git use GitHub CLI automatically
$ gh auth setup-git

This configures Git so:
no manual token entry
no password prompts
seamless push/pull


## Step 5: Intall and Initialize Git

$ sudo apt-get install git
$ git init

## Step 6: Configure Git (First Time Only)

```bash
$ git config --list
$ git config --global user.name "anisur81"
$ git config --global user.email "anisur81@gmail.com"

```

VS Code as the default Git editor.
```bash
$ git config --global core.editor "code --wait"

$  cd /mnt/g/WEB_PYTHON/django_proj/portfolio
$ git config  --list

user.name=anisur81
user.email=anisur81@gmail.com

core.editor=code --wait
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.ignorecase=true

credential.https://github.com.helper=
credential.https://github.com.helper=!/usr/bin/gh auth git-credential

credential.https://gist.github.com.helper=
credential.https://gist.github.com.helper=!/usr/bin/gh auth git-credential

remote.origin.url=https://github.com/anisur81/devsecops-portfolio.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*

```

## Step 6: Add and Commit Files
 
$ git add .
$ git commit -m "Initial commit"

## Step 7: Add GitHub Remote

Copy your repo HTTPS URL from GitHub, then run:

$ git remote add origin https://github.com/anisur81/devsecops-portfolio.git

## Step 8: Set Main Branch
git branch -M main

## Step 9: Push to GitHub

 ```bash
$ git push  origin main

Enumerating objects: 117, done.
Counting objects: 100% (117/117), done.
Delta compression using up to 20 threads
Compressing objects: 100% (113/113), done.
Writing objects: 100% (117/117), 260.53 KiB | 1.31 MiB/s, done.
Total 117 (delta 37), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (37/37), done.
To https://github.com/anisur81/devsecops-portfolio.git
 * [new branch]      main -> main

```

## Step 10: Future Updates
After changes:

$ git add .
$ git commit -m "Updated project"
$ git push origin main

## If Remote Already Exists
Check Current Remote
$ git remote -v

$ git remote remove origin
$ git remote add origin https://github.com/yourusername/my-devsecops-portfolio.git

## Clear Wrong Cached Credentials (Windows / WSL Common)

Because you're using Windows + WSL path (/mnt/g/...), old credentials may be cached.

Run:
$ git config --global --unset credential.helper 
$ git remote set-url origin <url>

## Meaning:

### You are changing an existing remote URL  

```bash
$ git remote set-url origin https://github.com/anisur81/devsecops-portfolio.git
$ git remote -v
origin  https://github.com/anisur81/devsecops-portfolio.git (fetch)
origin  https://github.com/anisur81/devsecops-portfolio.git (push)

```
## set-url command used when:

* You already have a remote named origin
* You want to switch:
* SSH → HTTPS
* old repo → new repo
* wrong URL → correct URL
