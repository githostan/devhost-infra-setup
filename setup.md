## DevHost Infrastructure Setup

# Initial Folder Structure 
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

# Updated PATH for DevOps Tools To Make PATH Export Persistent
- echo 'export PATH="$HOME/devops-tools/bin:$PATH"' >> ~/.bashrc 
source ~/.bashrc

# Applied it immediately:
- source ~/.bashrc

# Git Installation
- sudo apt update
- sudo apt install git -y

# Set Global Config:
- git config --global user.name "Your Full Name"
- git config --global user.email "your_email@example.com"

# Set default branch name (Optional):
- git config --global init.defaultBranch main

# Initialized Local Git Repo
- cd ~/infrastructure
- git init
- git add setup.md
- git commit -m "Initial infrastructure setup documentation"

# Created a New Repo on GitHub
- ·  Navigate to https://github.com/new
- ·  Created a New Repo on GitHub: devhost-infra-setup 
- ·  Left it empty — didn’t initialize with README, license, or .gitignore as we already have a repo locally.

# SSH Key Setup for GitHub
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

# Connectd Local Repo to GitHub
- Back in the terminal (Inside the ~/infrastructure project folder):
- git remote add origin git@github.com:githostan/devhost-infra-setup.git
- git remote set-url origin git@github.com:githostan/devhost-infra-setup.git

- You can confirm with:
-                 git remote -v

- It should now show:
-                origin  git@github.com:githostan/devhost-infra-setup.git (fetch)
-                origin  git@github.com:githostan/devhost-infra-setup.git (push)

# Final Push to GitHub
- git add setup.md
- git commit -m "Updated setup.md with SSH setup and GitHub push"
- git push -u origin main

---

## 🧰 Core Dev Tools Installation

# Installed Tools
- `curl`: Command-line tool for transferring data with URLs.
- `wget`: Non-interactive downloader for files from the web.
- `vim`: Lightweight terminal-based text editor.
- `htop`: Interactive process viewer (better than `top`).
- `tmux`: Terminal multiplexer for managing multiple sessions.
- `build-essential`: Compiler and build tools (gcc, make, etc.).

# Installation Command
- sudo apt update
- sudo apt install curl wget vim htop tmux build-essential -y

# After successful install, verified each:
- curl --version
- wget --version
- vim --version
- htop --version
- tmux -V
- gcc --version

# 📤 Push Changes to GitHub
- cd ~/infrastructure
- git add setup.md
- git commit -m "Installed and documented core DevOps CLI tools"
- git push -u origin main


## Installed Docker & Docker Compose

# Update package index
- sudo apt update

# Installed Docker and Docker Compose
- sudo apt install docker.io docker-compose -y

# Added my user to the docker group to avoid using sudo
- sudo usermod -aG docker $USER
- newgrp docker

# Verify installation
- docker --version
- docker-compose --version

# For the latest Docker Compose version, we installed it manually:
- sudo curl -L "https://github.com/docker/compose/releases/download/v2.38.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
- sudo chmod +x /usr/local/bin/docker-compose

# Installation verification
- docker-compose --version

# Tested Docker Installation
- docker run hello-world

---

# Pushed Changes to GitHub
- cd ~/infrastructure
- git add setup.md
- git commit -m "Installed and documented Docker & Docker Compose setup"
- git push -o original main

---
## Installed Kubernetes CLI Tools (kubectl, kubectx, kubens, k9s)
- These tools enhance your productivity when working with Kubernetes clusters as they make working with Kubernetes clusters a lot easier.

- Kubectl- for interacting with, and managing kubernetes clusters
- kubectx – for switching between clusters
- kubens – for switching between namespaces
- k9s – a powerful terminal UI to explore and manage your cluster


# ☸️ kubectl Manual Installation (v1.33.3)
# Reason
- Legacy APT repo deprecated.
- Manual install ensures latest version and avoids broken dependencies.

# Steps
- sudo apt update
- sudo apt install -y apt-transport-https ca-certificates curl

# Downloaded the latest stable version
- curl -LO "https://dl.k8s.io/release/$(curl -sL https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Made it executable
- chmod +x kubectl

# Move it to a system path
- sudo mv kubectl /usr/local/bin/

# Verified installation
- kubectl version --client

# Bonus: Enable Shell Autocompletion (Bash Completion)
- sudo apt install bash-completion -y
- echo 'source <(kubectl completion bash)' >> ~/.bashrc
- source ~/.bashrc

# Result
     ·  Installed kubectl (Client Version: v1.33.3)
     ·  Bash completion enabled
     ·  Bash completion enabled

# Installed kubectx and kubens (Use GitHub repo (official method))
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx
sudo ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx
sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens

# Optional bash completion for these:
ln -s /opt/kubectx/completion/kubens.bash ~/.kubens-completion.bash
ln -s /opt/kubectx/completion/kubectx.bash ~/.kubectx-completion.bash

echo 'source ~/.kubens-completion.bash' >> ~/.bashrc
echo 'source ~/.kubectx-completion.bash' >> ~/.bashrc
source ~/.bashrc

# Installed k9s
# Downloaded latest release:
curl -LO https://github.com/derailed/k9s/releases/latest/download/k9s_Linux_amd64.tar.gz

# Extract and install:
tar -xzf k9s_Linux_amd64.tar.gz
sudo mv k9s /usr/local/bin/
rm k9s_Linux_amd64.tar.gz

# Verify:
k9s version

# Notes
- kubens and kubectx require a valid Kubernetes context to function.
- kubens does not support a --version flag.
- K9s installed successfully (v0.50.9).
- These tools will become active once a cluster is installed (next step).

# Pushed Changes to GitHub
     ·  cd ~/infrastructure
     ·  git add setup.md
     ·  git commit -m "Installed and documented kubectl, kubectx, kubens, and K9s"
     ·  git push -o original main









