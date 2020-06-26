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
sudo docker build -t netsoft2020tutorial4demo3exp3 .
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
    <img src="images/images_d2_e2.png"/> 
</p>

We can check if the containers are up:
```
sudo docker-compose ps
```
The output should be similar to the following:
<p align="center">
    <img src="images/containers_d2_e2.png"/> 
</p>

The first step of the experiment is to store in HSS the UE's information using the Web Interface of the [free5GC](https://www.free5gc.org/) project that is available at http://localhost:3000, as is shown in the image below.
<p align="center">
    <img src="images/login.png" height="450"/> 
    <img src="images/webapp.png"/> 
</p>

We use the [openSTF](https://openstf.io/) tool to access the smartphone remotely.
This software is available at http://localhost:7100, as is shown in the image below.
<p align="center">
    <img src="images/openSTF.png" height="450" width="450"/> 
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


--> Colocar o celular em modo gateway

--> Começar a parte do LoRa


--> Lúcio revisar. Precisamos ver se essa configuração fará parte da seção de instalação o teste.

***Add a LoRa® gateway***

There are two steps involved when adding a gateway. First of all, you need to configure your gateway so that it sends data to the ChirpStack Gateway Bridge component. In the packet-forwarder configuration, modify the following configuration keys:

server_address to the IP address / hostname of the ChirpStack Gateway Bridge
serv_port_up to 1700 (the default port that ChirpStack Gateway Bridge is using)
serv_port_down to 1700 (same)

The second step is to add the LoRa gateway to your ChirpStack Server network. For this, log in into the ChirpStack Application Server web-interface and add the gateway to your organization. In case your gateway does not have a GPS, you can set the location manually.

todo figura

***Setting up your first LoRaWAN® device***

Now all ChirpStack components are installed, you should be able to navigate to the ChirpStack Application Server web-interface.

To access the ChirpStack Application Server web-interface, enter the IP address or hostname of you server, followed by port 8080.

Example: https://localhost:8080/.

Once you have the interface working, you are ready to add the configurations required in order to receive data from a device.

****Add network-server****

In order to connect your ChirpStack Application Server instance with the ChirpStack Network Server instance, click Network servers and then Add.

As each container has its own hostname, you must use the hostname of the networkserver container when adding the network-server in the ChirpStack Application Server web-interface. (sudo docker ps)

<p align="center">
    <img src="images/lorawan_add_nt_server.png"/> 
</p>

When using the above example, it means that you must enter lorawan_chirpstack-network-server_1:8000 as the network-server hostname:Port.


****Service Profile****

The service-profile defines the features that can be used by an organization.

Click on Service-profiles and then Create to create a service-profile for the ChirpStack organization. This will also associate the organization with the network-server instance.

****Device Profile****

The device-profile defines the device properties of a device. For example it defines the activation type (OTAA vs ABP), the implemented LoRaWAN version etc…

Click on Device-profiles and then Create to create a device-profile for the ChirpStack organization.

****Application****

Now that there is a ChirpStack Application Server / ChirpStack Network Server association, a service-profile for the organization and device-profile, it is time to create your first application.

Click on Applications, then click on Create.

Next, click on the created application to see the list of devices associated with this application. This will be an empty list until you complete the next step…

****Device****

Click on the Devices tab (found under Application/YourApp if you aren’t there already), then click on the Create button to create a new device.

After the creation of an Over the Air Activation (OTAA) device, you will be redirected to a page where you can enter the root key(s). After the creation of an Activation By Personalization (ABP) device, you will be redirected to a page where you can enter the session keys. The selected Device Profile that was created in the steps above determines whether the device uses OTAA or ABP.

Check that you are receiving data
It is possible to stream all LoRaWAN frames (raw and encrypted data) and device data from the web-interface. Click on the created device and click on the live data or LoRaWAN frames tab. Now it is time to turn on your device and start receiving data!


In this experiment, RAN is deployed with the Software Radio Systems LTE project, i.e., LTE. The Core is implemented using the free5GC project. This experiment's main goal is to demonstrate a connection between UE in hardware (LoRaWAN Gateway with LTE interface ), 4G RAN in hardware (SDR - Software-Defined Radio) and software, and 5G SBA core implemented in software.