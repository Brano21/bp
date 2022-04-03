# bp-DNS_Rebinding

Here you can download VMs and the resources you need to run the attacker web server site.

## Introduction
In this lab, students should gain first-hand experience on how to use the DNS rebinding technique to attack IoT devices. In the topology.png file, you can see that this lab contains 4 virtual machines. First is a router with a 10.10.30.1 IP address, second is a client (the victim) with a 10.10.30.5 IP address, third is an attacker (you) with 10.10.30.6 and last is a server with 10.10.30.7 IP address. Your job is to get access to the thermometer, which is running on the client's virtual machine, and set the temperature.

## How DNS rebinding work
The attack targets Internet of Things (IoT) devices. Many of them do not have very sophisticated protection schemes. If an attacker manages to communicate with these IoT devices, he will likely be able to exploit the vulnerabilities of these devices.
##### The firewall - 
an attacker can not directly access the IoT device and if he wanted to he will be blocked by a firewall because this IoT device is a private IP address that is not accessible from the outside. The only way an attacker can access this IoT device is to talk to the IoT device from the local environment. An attacker must be on the same network behind the firewall to access it. This issue could be resolved by a client's visiting the attacker's website. What the attacker has to do is send an e-mail or advertisement to the user and if the user clicks on the given link he will go to the attacker's website.
##### The same origin policy - 
ensures that the user can interact with their server. For IoT device (thermostat) we will give an example of a website called termostat.com. Thanks to a policy of the same origin, the thermostat will be able to communicate with termostat.com. However, if an attacker uses his site (attacker.com) to try to communicate with the Internet of Things server, it is a request from two different sources. This is because the attacker uses attacker.com and thermostat termostat.com. Therefore, the browser does not allow the attacker to retrieve the data. But one thing needs to be realized. The same-origin policy only checks names, not IP addresses. Therefore, if the user could obtain the IP address of the thing, the thermostat, he would be able to set the temperature on it.

## Installation
Firstly, you need to copy this repository into your computer. After downloading access the folder and navigate to the **muni-kypo_VMs** folder. Run this command: 
<br />
*create-sandbox --provisioning-dir ./provisioning ./rebinding.yml*
<br />
this should create the intermediate sandbox definition. Navigate to the **sandbox** folder and run this command:
<br />
*manage-sandbox build*
<br />
after a while, three virtual machines will be displayed in the virtual box - router, server-wan and attacker.
<br />
Now you need to build the last one - Client. Navigate to **vagrant_VMs/server** folder which is located in your downloaded folder. Run this command:
<br />
*vagrant up*
<br />
after a while, you should see the Client in the virtual box. For the first time, you turn off this machine and turn it on again. This is important because for the first time this machine does not connect to the network.

## Tasks
Firstly you need to start the bash script on the client VM. Start the bash start script - start.sh and after a while, the firefox browser should start on. Then visit the attacker website attacker32.com:8080
<br /><br />
On the attacker machine:
1. Go to rebinding_repo
2. Copy attacker.com.zone to /etc/bind folder
3. Copy content of _etc_bind to /etc/bind/named.conf
4. Restart bind9 service and check if bind9 is running
5. Unzip attacker_vm zip
6. Navigate to attacker_vm folder
7. Add URL prefix 'attacker32.com' to the change.js file
8. Restart bind9

Switch back to the client VM and refresh www.attacker32.com and continue on the attacker machine

9. Change the IP address of www.attacker32.com in the /etc/bind/attacker.com.zone
10. Restart bind9

### Resources
https://seedsecuritylabs.org/Labs_16.04/PDF/DNS_Rebinding.pdf
