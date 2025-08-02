## DevHost Infrastructure Setup

## Initial Folder Structure 
- Created directory structure:  ~/devops-tools/ with subfolders: 
- mkdir -p ~/devops-tools/{bin,configs,scripts,logs,docs,projects}
- mkdir -p ~/infrastructure
- touch ~/infrastructure/setup.md

- This gives you:
-     ·  bin/: Custom binaries or symlinks
-     ·  configs/: Config files (e.g., kubeconfig, .tool-versions)
-     ·  scripts/: Shell scripts for automation
-     ·  logs/: For storing output logs (logging)
-     ·  docs/: Markdown notes
-     ·  projects/: Your deployments or experiments

##  Update PATH for DevOps Tools To Make PATH Export Persistent
- echo 'export PATH="$HOME/devops-tools/bin:$PATH"' >> ~/.bashrc 
source ~/.bashrc

## Apply it immediately:
- source ~/.bashrc

## Git Installation
- sudo apt update
- sudo apt install git -y

## Set Global Config:
- git config --global user.name "Your Full Name"
- git config --global user.email "your_email@example.com"

## Optional - Set default branch name:
- git config --global init.defaultBranch main

## Initialize Local Git Repo
- cd ~/infrastructure
- git init
- git add setup.md
- git commit -m "Initial infrastructure setup documentation"

## Create a New Repo on GitHub
- ·  Navigate to https://github.com/new
- ·  Created a New Repo on GitHub: devhost-infra-setup 
- ·  Left it empty — didn’t initialize with README, license, or .gitignore as we already have a repo locally.

## SSH Key Setup for GitHub
- Note- If you're using SSH keys, this will push your repo without needing username/password. If you're using HTTPS, GitHub may prompt you to authenticate

- Generate a new SSH key
- ssh-keygen -t ed25519 -C "github.mini_pc"

- ·  When prompted:
-          o  Save to default location (accept default path): just press Enter
-          o  Optional passphrase: press Enter again or add one if you prefer
- This generates:
-     ·  ~/.ssh/id_ed25519 (private key — do not share)
-     ·  ~/.ssh/id_ed25519.pub (public key — this goes to GitHub)
- Then:
-     ·  cat ~/.ssh/id_ed25519.pub       # displays your public key

- Copy the output and go to GitHub ➜
- Profile photo → Settings → SSH and GPG keys → New SSH key
-     ·  Title: mini-pc
-     ·  Paste key ➜ Save

- Test SSH to GitHub from both Mini-PC Server
-     ·  ssh -T git@github.com

- You should see:
-               Hi githostan! You've successfully authenticated, but GitHub does not provide shell access.

## Connect Your Local Repo to GitHub
- ·  Back in your terminal (Inside your ~/infrastructure project folder):
- git remote add origin git@github.com:githostan/devhost-infra-setup.git
- git remote set-url origin git@github.com:githostan/devhost-infra-setup.git

- You can confirm with:
-                 git remote -v

- It should now show:
-                origin  git@github.com:githostan/devhost-infra-setup.git (fetch)
-                origin  git@github.com:githostan/devhost-infra-setup.git (push)

## Final Push to GitHub
- git add setup.md
- git commit -m "Updated setup.md with SSH setup and GitHub push"
- git push -u origin main
