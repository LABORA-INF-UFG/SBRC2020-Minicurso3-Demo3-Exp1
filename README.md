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

On the first VM or MiniPC where the SDR is connected.


To build the eNB and all 5GC images, use the following command:  
```
$ sudo docker build -t netsoft2020tutorial4demo2exp2 .  todoooo
```

We can check if the images are up:
```
$ sudo docker image ls
```
The output should be similar to the following:
<p align="center">
    <img src="images/images_d2_e2.png"/> 
</p>

To run the containers, use the following command:
```
$ sudo docker-compose up -d
```

We can check if the containers are up:
```
$ sudo docker-compose ps
```
The output should be similar to the following:
<p align="center">
    <img src="images/containers_d2_e2.png"/> 
</p>

Done! The software is successfully installed.

# 3 - Build the images and running the containers LoRaWAN 

On te second VM or Cloud, repeat all Step 1.

```
cd  NetSoft2020-Tutorial4-Demo3-Exp1/LoRaWAN$
```
Run
```
sudo docker-compose up -d
```

<p align="center">
    <img src="images/lorawan_docker_result.png"/> 
</p>


***Add a LoRa® gateway

There are two steps involved when adding a gateway. First of all, you need to configure your gateway so that it sends data to the ChirpStack Gateway Bridge component. In the packet-forwarder configuration, modify the following configuration keys:

server_address to the IP address / hostname of the ChirpStack Gateway Bridge
serv_port_up to 1700 (the default port that ChirpStack Gateway Bridge is using)
serv_port_down to 1700 (same)

The second step is to add the LoRa gateway to your ChirpStack Server network. For this, log in into the ChirpStack Application Server web-interface and add the gateway to your organization. In case your gateway does not have a GPS, you can set the location manually.

todo figura

***Setting up your first LoRaWAN® device

Now all ChirpStack components are installed, you should be able to navigate to the ChirpStack Application Server web-interface.

To access the ChirpStack Application Server web-interface, enter the IP address or hostname of you server, followed by port 8080.

Example: https://localhost:8080/.

Once you have the interface working, you are ready to add the configurations required in order to receive data from a device.

****Add network-server

In order to connect your ChirpStack Application Server instance with the ChirpStack Network Server instance, click Network servers and then Add.

As each container has its own hostname, you must use the hostname of the networkserver container when adding the network-server in the ChirpStack Application Server web-interface. (sudo docker ps)

<p align="center">
    <img src="images/lorawan_add_nt_server.png"/> 
</p>

When using the above example, it means that you must enter lorawan_chirpstack-network-server_1:8000 as the network-server hostname:Port.


****Service Profile
The service-profile defines the features that can be used by an organization.

Click on Service-profiles and then Create to create a service-profile for the ChirpStack organization. This will also associate the organization with the network-server instance.

****Device Profile
The device-profile defines the device properties of a device. For example it defines the activation type (OTAA vs ABP), the implemented LoRaWAN version etc…

Click on Device-profiles and then Create to create a device-profile for the ChirpStack organization.

****Application
Now that there is a ChirpStack Application Server / ChirpStack Network Server association, a service-profile for the organization and device-profile, it is time to create your first application.

Click on Applications, then click on Create.

Next, click on the created application to see the list of devices associated with this application. This will be an empty list until you complete the next step…

****Device
Click on the Devices tab (found under Application/YourApp if you aren’t there already), then click on the Create button to create a new device.

After the creation of an Over the Air Activation (OTAA) device, you will be redirected to a page where you can enter the root key(s). After the creation of an Activation By Personalization (ABP) device, you will be redirected to a page where you can enter the session keys. The selected Device Profile that was created in the steps above determines whether the device uses OTAA or ABP.

Check that you are receiving data
It is possible to stream all LoRaWAN frames (raw and encrypted data) and device data from the web-interface. Click on the created device and click on the live data or LoRaWAN frames tab. Now it is time to turn on your device and start receiving data!
