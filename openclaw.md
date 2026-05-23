# OpenClaw Setup

# Update

```
sudo apt update && sudo apt dist-upgrade
```

# Install basic tools

https://github.com/eliranwong/ChromeOSLinux/blob/main/README.md#basic-tools--libaries

# Install ollama

Read more at https://ollama.com

```
# Install dependency
sudo apt install zstd
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh
# Sign in
ollama singin
# Pull cloud model
ollama pull glm-5.1:cloud
# Copy the signature key from /usr/share/ollama/.ollama/id_ed25519 to ~/.ollama/
mkdir -p ~/.ollama/
sudo cp /usr/share/ollama/.ollama/id_ed25519 ~/.ollama/
sudo chown $USER:$USER ~/.ollama/id_ed25519
chmod 600 ~/.ollama/id_ed25519
```

# Install Docker Engine

Read more at https://docs.docker.com/engine/install/debian/

```
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
# Install docker engine
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
# add user to docker group
sudo usermod -aG docker $LOGNAME
newgrp docker
```

# Install SearXNG to work with OpenClaw web search

Read more at https://docs.searxng.org/admin/installation-docker.html#installation-container

```
mkdir -p ./searxng/core-config/
cd ./searxng/
curl -fsSL \
    -O https://raw.githubusercontent.com/searxng/searxng/master/container/docker-compose.yml \
    -O https://raw.githubusercontent.com/searxng/searxng/master/container/.env.example
cp -i .env.example .env
# edit the default port
sed -i 's/^#SEARXNG_PORT=8080/SEARXNG_PORT=4000/' .env
# start the service
docker compose up -d
```

# Install discord

1. Set up apparmor service

```
# start apparmor service
sudo systemctl start apparmor
sudo systemctl enable apparmor
```

2. Download at https://discord.com/download
3. Copy to Linux Files directory and run `sudo apt install ./discord...`

# Install Document Conversion Tools

```
sudo apt install pandoc texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended texlive-xetex
```

# Install Node

Follow download script at https://nodejs.org/en/download

```
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
# in lieu of restarting the shell
source ~/.bashrc
# Download and install Node.js:
nvm install 24
```

# Install OpenClaw

```
npm install -g mcporter@latest
npm install -g clawhub@latest
npm install -g @steipete/summarize@latest
npm install -g @mariozechner/pi-ai@latest
npm install -g openclaw@latest
ollama launch openclaw --config
openclaw onboard --install-daemon
```

Remarks:

* skip provider; use current value for provider
* select discord as channel
* select searxng for web search tool and enter http://localhost:4000/

# Optional

## Install Coding Agents

Read https://github.com/eliranwong/AMD_iGPU_AI_Setup/blob/main/coding_agents.md

## Install Antigravity

Download Antigravity from https://antigravity.google/

```
tar -xvzf Antigravity.tar.gz
sudo mv Antigravity-x64 /opt/antigravity
sudo chown root:root /opt/antigravity/chrome-sandbox
sudo chmod 4755 /opt/antigravity/chrome-sandbox
sudo ln -s /opt/antigravity/antigravity /usr/local/bin/antigravity
```
