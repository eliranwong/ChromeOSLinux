# Install Docker

> sudo apt update && sudo apt dist-upgrade

> sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common

> curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

> sudo apt-key fingerprint 0EBFCD88

> sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

> sudo apt update

> sudo apt install docker-ce docker-ce-cli containerd.io

> sudo docker run hello-world

More at:

https://dvillalobos.github.io/2020/How-to-install-and-run-Docker-on-a-Chromebook/

https://docs.docker.com/engine/install/debian/

# Clean docker cache

> docker system prune --volumes

More at:

https://renehernandez.io/snippets/cleaning-local-docker-cache/
