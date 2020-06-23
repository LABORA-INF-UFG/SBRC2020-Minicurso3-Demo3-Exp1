# NetSoft2020-Tutorial4-Demo3-Exp1
NetSoft2020-Tutorial4-Demo3-Exp1

## Expected result

ToDo ....
<p align="center">
    <img src="images/demo3-exp1.png"/> 
</p>

## Installation

**Requirements**

The installation can be done directly over the host operating system (OS) or inside a virtual machine (VM). System requirements:
* CPU type: x86-64 (specific model and number of cores only affect performance)
* RAM: 4 GB
* Disk space: 40 GB
* Ubuntu 18.04 LTS

**Using Docker Compose**

Docker Compose (part of Docker) makes it possible to orchestrate the configuration of multiple Docker containers at once using a docker-compose.yml file.

***Install Docker***

Older versions of Docker were called docker, docker.io, or docker-engine. If these are installed, uninstall them:
'''
$ sudo apt-get remove docker docker-engine docker.io containerd runc
'''
Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1 - Set up the Repository

Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```    
Add Docker’s official GPG key:

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Use the following command to set up the stable repository.

```
 sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
 ```  
 
2 - Install Docker Engine
Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:

```
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

 Verify that Docker Engine is installed correctly by running the hello-world image.
 
```
$ sudo docker run hello-world
```

***Install Compose***

On Linux, you can download the Docker Compose binary from the Compose repository release page on GitHub. 

Run this command to download the current stable release of Docker Compose:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
Apply executable permissions to the binary:

```
sudo chmod +x /usr/local/bin/docker-compose
```
Test the installation.

```
$ docker-compose --version
docker-compose version 1.26.0, build 1110ad01
```
