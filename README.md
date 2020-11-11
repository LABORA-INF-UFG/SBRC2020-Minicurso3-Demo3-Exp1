# SBRC2020-Minicurso3-Demo3-Exp1

## Expected result
This experiment aims to demonstrate a RAN based on LTE technology with integrated with a LoRa wireless network implemented in hardware (non-3GPP Network). For RAN LTE, we use open-source software and an SDR. We also use an open-source implementation of the SBA-based 5G core software, as illustrated by the following image.
<p align="center">
    <img src="images/demo3-exp1.png" height="300"/> 
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
* LoRaWAN Gateway
* LoRaWAN Node

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
git clone https://github.com/LABORA-INF-UFG/SBRC2020-Minicurso3-Demo3-Exp1.git

```

To build the eNB and all 5GC images, use the following command:  
```
sudo docker build -t sbrc2020Minicurso3demo3exp1 .
```

To run the containers, use the following command:
```
sudo docker-compose up -d
```

To build the LoRaWAN imagens, we use a Virtal Machine in the cloud and the following the commands:
```
git clone https://github.com/LABORA-INF-UFG/SBRC2020-Minicurso3-Demo3-Exp1.git
```

```
cd  SBRC2020-Minicurso3-Demo3-Exp/LoRaWAN
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
    <img src="images/network.png" height="450" width="300"/> 
    <img src="images/ping.png" height="450"/> 
</p>

We connect the smartphone to the gateway via USB. This smartphone is placed in USB Tethering mode to make the connection via the cellular network.
<p align="center">
    <img src="images/tethering.png" height="450" width="300"/> 
    <img src="images/gateway_phone.png" height="450" width="300"/> 
</p>

Finally, we have the network configured.
<p align="center">
    <img src="images/device_connected.png" height="450"/> 
</p>

We can see the data received from the sensor in the LoRaWAN application server.
<p align="center">
    <img src="images/device_test.png"/> 
</p>



## Additional comments

Two steps are needed when adding a gateway LoRa. 

1. To configure the gateway that it sends data to the ChirpStack Gateway Bridge component. In the packet-forwarder configuration, modify the following configuration keys:
```
server_address to the IP address / hostname of the ChirpStack Gateway Bridge
serv_port_up to 1700 (the default port that ChirpStack Gateway Bridge is using)
serv_port_down to 1700 (same)
```
More details on installing the gateway with the Raspberry Pi in the [product manual](https://resource.heltec.cn/download/HT-M01/ht-m01_user_manual.pdf).

2. To add the LoRa gateway to the ChirpStack Server network. For this, access the ChirpStack Application Server web-interface (http://IP:8080) and add the gateway with the following steps. 

<p align="center">
    <img src="images/login_chirpstack.png"  height="450"/> 
</p>

To connect the ChirpStack Application Server instance with the ChirpStack Network Server instance, click Network servers and after click in Add.
<p align="center">
    <img src="images/lorawan_add_nt_server.png"/> 
</p>

To create a service profile.
<p align="center">
    <img src="images/lorawan_service_profile.png"/> 
</p>

To add the gateway ID that will be managed, after adding the Service Profile.
<p align="center">
    <img src="images/lorawan_gateway_add.png"/> 
</p>

To configure the Gateway Profile.
<p align="center">
    <img src="images/lorawa_gwprofile_add.png"/> 
</p>

The LoRaWAN gateway must be functional if the following information appears.
<p align="center">
    <img src="images/lorawan_gateway_test.png" height="450"/> 
</p>

To configure the sensors that we want to monitor, add a profile for the device.
<p align="center">
    <img src="images/device_profile.png"/> 
</p>

The device must be associated with an application, so we must create it.
<p align="center">
    <img src="images/device_application.png"/> 
</p>


We can add the device to the application. 
<p align="center">
    <img src="images/device_add.png"/> 
</p>


We need to configure the corresponding hardware device address.

<p align="center">
    <img src="images/device_add_config.png"/> 
</p>

LoRaWAN software network components were provided by the [chirpstack](https://www.chirpstack.io/) project.

The LoRaWAN sensor is a [generic microcontroller](https://heltec.org/project/wifi-lora-32/) with a lora radio interface. It uses the following [sample software](https://github.com/LABORA-INF-UFG/NetSoft2020-Tutorial4-Demo3-Exp1/blob/master/LoRaWAN/lora_nodo_code.ino)

The SIM card used is of [sysmocom](https://www.sysmocom.de/index.html) with an Android Samsung Galaxy S7 SM-G930F.

SDR is an [Ettus B210](https://www.ettus.com/) with four antennas connected via USB in the mini PC.  

RAN is deployed with the [Software Radio Systems LTE](https://github.com/srsLTE/srsLTE) project.

The Core is implemented using the [free5GC](https://www.free5gc.org/) project.
