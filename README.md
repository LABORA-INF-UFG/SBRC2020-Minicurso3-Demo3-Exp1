# NetSoft2020-Tutorial4-Demo3-Exp1

## Expected result
This experiment aims to demonstrate a RAN based on LTE technology with integrated with a LoRa wireless network implemented in hardware (non-3GPP Network). For RAN LTE, we use open-source software and an SDR. We also use an open-source implementation of the SBA-based 5G core software, as illustrated by the following image.
<p align="center">
    <img src="images/demo3-exp1.png"/> 
</p>

 ## Installation

**Requirements**

The minimum hardware requirement and software to run this experiment is shown in the image below.
* Sensor LoRa
* Mini Gateway LoRa
* Smartphone Android
* SIM card (writable)
* USRP B210
* Mini PC (RAM: 4GB and disk space: 40GB)
* Ubuntu 16.04 LTS
* Docker 18.09.7
* srsLTE release 19_12
* free5GC stage 1
* ChirpStack 

**Steps**

We need two tools to run this experiment, _Git_ and _Docker_

To install _Git_, run the following command:
```
sudo apt-get install git-all
```

To install _Docker_, run the following commands:
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

 After, we can clone the **NetSoft2020-Tutorial4-Demo3-Exp1 project**:
```
git clone https://github.com/LABORA-INF-UFG/NetSoft2020-Tutorial4-Demo3-Exp1.git
```

To build the eNB and all 5GC images, use the following command:  
```
sudo docker build -t netsoft2020tutorial4demo3exp1 .
```

To run the containers, use the following command:
```
sudo docker-compose up -d
```

To build the LoRaWAN imagens, we use a Virtal Machine in the cloud and the following the commands:
```
git clone https://github.com/LABORA-INF-UFG/NetSoft2020-Tutorial4-Demo3-Exp1.git
```

```
cd  NetSoft2020-Tutorial4-Demo3-Exp1/LoRaWAN
```

```
sudo docker-compose up -d
```
<p align="center">
    <img src="images/lorawan_docker_result.png"/> 
</p>

Done! The software is successfully installed.

## Tests

We can check if the images are up:
```
sudo docker image ls
```
The output should be similar to the following:
<p align="center">
    <img src="images/images_d3_e1.png"/> 
</p>

We can check if the containers are up:
```
sudo docker-compose ps
```
The output should be similar to the following:
<p align="center">
    <img src="images/containers_d3_e1.png"/> 
</p>

The first step of the experiment is to store in HSS the UE's information using the Web Interface of the [free5GC](https://www.free5gc.org/) project that is available at http://localhost:3000, as is shown in the image below.
<p align="center">
    <img src="images/login.png" height="450"/> 
    <img src="images/webapp.png"/> 
</p>

We can see the smartphone connected in the network called free5GC available. 
<p align="center">
    <img src="images/connectedfree5GC.png" height="450"/> 
</p>

We use the [PingTools Network Utilities](https://play.google.com/store/apps/details?id=ua.com.streamsoft.pingtools&hl=pt_BR) tool available at GooglePlay to test the connectivity of the network.
<p align="center">
    <img src="images/network.png" height="450"/> 
    <img src="images/ping.png" height="450"/> 
</p>


We connect the phone to the gateway via USB. Then the phone is placed in USB Tethering mode, to make the connection via the cellular network.
<p align="center">
    <img src="images/tethering.png" height="450"/> 
    <img src="images/gateway_phone.png" height="450"/> 
</p>

***Setting  LoRaWAN® Network***

Now all LoRaWAN components are installed. We need to configure the network through the web interface. http://IP:8080

We connect ChirpStack Application Server instance with the ChirpStack Network Server instance, click Network servers and then Add.

<p align="center">
    <img src="images/lorawan_add_nt_server.png"/> 
</p>

We need create a service profile

<p align="center">
    <img src="images/lorawan_service_profile.png"/> 
</p>

After adding the Service Profile, we need to add the gateway ID that will be managed

<p align="center">
    <img src="images/lorawan_gateway_add.png"/> 
</p>

We need  configure Gateway Profile

<p align="center">
    <img src="images/lorawan_gwprofile_add.png"/> 
</p>

<p align="center">
    <img src="images/lorawan_gateway_test.png"/> 
</p>
.........

<p align="center">
    <img src="images/device_profile.png"/> 
</p>

<p align="center">
    <img src="images/device_application.png"/> 
</p>

<p align="center">
    <img src="images/device_add.png"/> 
</p>

<p align="center">
    <img src="images/device_add_config.png"/> 
</p>


<p align="center">
    <img src="images/device_connected.png"/> 
</p>


<p align="center">
    <img src="images/device_test.png"/> 
</p>


