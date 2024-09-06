# Docker Installation on Ubuntu

This guide provides the steps to install Docker on an Ubuntu server in one go.

```bash
# Update the package index and install required packages to allow apt to use a repository over HTTPS.
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

# Add Docker’s official GPG key.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Set up the Docker repository.
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Update the package index again.
sudo apt-get update

# Install Docker CE (Community Edition).
sudo apt-get install docker-ce

# Verify that Docker is installed correctly by checking the version.
sudo docker --version

# Add the current user to the docker group to avoid typing sudo for Docker commands.
sudo usermod -aG docker ${USER}
newgrp docker

# Run a test container to ensure Docker is set up correctly.
docker run hello-world

# Enable Docker to start on boot, and start the Docker service.
sudo systemctl enable docker
sudo systemctl start docker
```

## Install Docker Compose
At the time of this writing, the most current stable version is 2.3.3. Use the following command to download:

```sh
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
```

Next, set the correct permissions so that the `docker compose` command is executable:

```sh
chmod +x ~/.docker/cli-plugins/docker-compose
docker compose version
```
