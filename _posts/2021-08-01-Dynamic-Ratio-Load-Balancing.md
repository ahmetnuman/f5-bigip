---
layout: post
tags: Dynamic Ratio Load Balancing
title: Dynamic Ratio Load Balancing
categories: f5-ltm
---

We can adjust load balancing ratio according to servers consuming resource such as CPU, Memory and Disk.

In this lab i will be apply this scenario :

- F5 will monitor server resources via SNMP Agent
- then F5 will assign ratio on the nodes dynamicaly and perform load balancing 

Here is the lab topology ;

---

![Image](/img/dynamicratio.png)

## On the Window Servers Perfom Following Task

- Assign IP address, subnet mask and default gw
- Windows firewall disable
- Run IIS Servive
- Run SNMP Service and configure security strings : TEST , allow IP : any

---

## On the F5

- Create SNMP DCA monitor, to accomplish that **Local Traffic >> Monitor >> Create**
  - Name : snmp_dca_monitor
  - Community : TEST
  - Version : v2c
  - Agent Type : WIN2000

other setting will be remain default or whatever you want.

![Image](/img/dcamonitor.png)

---

- Assign nodes and add monitor them with snmp_dca_agent **Local Traffic > Nodes > Create**

![Image](/img/node1.png)

all other two nodes added same way

---

- Crete Pool with Load Balancing Method Dynamic Ratio (nodes) and assign pool members and monitor pool member with http

![Image](/img/pool1.PNG)
![Image](/img/pool.PNG)

---

- Cretae VS Server 
  - IP Address : 192.168.138.200
  - Service Port : 80
  - Default Pool : test-web-pool

![Image](/img/vs.PNG)
![Image](/img/vs2.PNG)

---

- Verify dynamic ratio rates from F5 cli

`tmsh list ltm nodes dynamic-ratio`

![Image](/img/ver1.PNG)

At this moment server 1 resources : 

![Image](/img/server1.PNG)

At this moment server 2 resources : 

![Image](/img/server2.PNG)

At this moment server 3 resources :

![Image](/img/server3.PNG)

---

- Enable and view snmp dca agent logs on the F5

**from cli**

 `tmsh modify /sys db snmp.snmpdca.log value true`

 `cat /shared/tmp/snmpdca.log`

- Perform Syn flood from layer 2 network with hping3 and check the dynamic ratio rates from cli.

`hping3 -c 15000 -d 120 -S -w 64 -p 80 --flood --rand-source 20.20.20.21`

![Image](/img/hping3.PNG)

`tmsh list ltm node dynamic-ratio`

![Image](/img/ver2.PNG)

At this time server 1 resources

![Image](/img/ver3.PNG)