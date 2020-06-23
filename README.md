# NetSoft2020-Tutorial4-Demo3-Exp1
NetSoft2020-Tutorial4-Demo3-Exp1

## Expected result
This experiment aims to demonstrate a RAN based on LTE technology with integrated with a LoRa wireless network implemented in hardware (non-3GPP Network). For RAN LTE, we use open-source software and an SDR. We also use an open-source implementation of the SBA-based 5G core software, as illustrated by the following image.
<p align="center">
    <img src="images/demo3-exp1.png"/> 
</p>

In this experiment, RAN is deployed with the Software Radio Systems LTE project, i.e., LTE. The Core is implemented using the free5GC project. This experiment's main goal is to demonstrate a connection between UE in hardware (LoRaWAN Gateway with LTE interface ), 4G RAN in hardware (SDR - Software-Defined Radio) and software, and 5G SBA core implemented in software.

The minimum hardware requirement and software to run this experiment is shown in the image below.

todo...

For this experiment, we assume that the machines has full access to the Internet.

# 1 - Installation tools

**Requirements**

The installation can be done directly over the host operating system (OS) or inside 2 virtual machines (VMs). System requirements:
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
docker-compose version 1.26.0, build d4451659
```

After, we can clone the **NetSoft2020-Tutorial4-Demo3-Exp1 project**:
```
$ git clone https://github.com/LABORA-INF-UFG/NetSoft2020-Tutorial4-Demo3-Exp1.git
```

# 2 - Build the images and running the containers eNB and free5G


# 3 - Build the images and running the containers LoRaWAN 

In te second VM or Cloud, repeat all Step 1.

```
cd  NetSoft2020-Tutorial4-Demo3-Exp1/LoRaWAN$
```
Run
```
sudo docker-compose up -d
```
