# Complete Guide to Creating and Pushing Docker Images to Amazon ECR

# step 1:- first we need docker on top of ubuntu system

# Install using the apt repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1: Set up Docker's apt repository

#Add Docker's official GPG key:

$sudo apt-get update

$sudo apt-get install ca-certificates curl

$sudo install -m 0755 -d /etc/apt/keyrings

$sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

$sudo chmod a+r /etc/apt/keyrings/docker.asc

#Add the repository to Apt sources:

$echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
$sudo apt-get update

![Screenshot (383)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/74b25148-89cd-4c16-bd0d-3040a005ffb1)

2: To install the latest version, run:

$sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

3: Verify that the Docker Engine installation is successful by running the hello-world image.

$sudo docker run hello-world
