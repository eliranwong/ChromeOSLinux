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

# Build Unique Bible App docker image

> git clone https://github.com/eliranwong/uniquebibleapp-webtop.git

> cd uniquebibleapp-webtop

> sudo docker build -t uniquebibleapp .

# Run docker image

e.g. uniquebibleapp

> sudo docker run -d --name=uniquebibleapp --security-opt seccomp=unconfined -e PUID=1000 -e PGID=1000 -e TZ=Europe/London -e SUBFOLDER=/ -e KEYBOARD=en-gb-qwerty -p 3000:3000 -v ~/uniquebibleapp-webtop:/config -v /var/run/docker.sock:/var/run/docker.sock --shm-size="1gb" --restart unless-stopped uniquebibleapp

# Share docker image

e.g. uniquebibleapp image

Create a repository at https://hub.docker.com/

> sudo docker login -u username

Enter password

> sudo docker tag uniquebibleapp [username]/uniquebibleapp

> sudo docker push [username]/uniquebibleapp

# Remove Unique Bible App docker image

> sudo docker rm -f uniquebibleapp

Check uniquebibleapp image id with:

> sudo docker images

Remove image file

> sudo docker rmi [imageid]

Remove uniquebibleapp data, depending on what local path you specified in docker build command, e.g.:

> rm -rf ~/uniquebibleapp-webtop

# Clean docker all types of cache

> docker system prune --volumes

More at:

https://renehernandez.io/snippets/cleaning-local-docker-cache/
