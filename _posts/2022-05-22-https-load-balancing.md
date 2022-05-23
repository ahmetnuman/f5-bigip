---
layout: post
tags: https load baalncing
title: https load balancing
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 22.05.2022 , Ankara-Turkey

## Lab 3.3 HTTPS Load Balancing

- **Task 1 : Import SSL Certficate and Key To the BigIP**  

Navigate to **System  ››  Certificate Management : Traffic Certificate Management : SSL Certificate List  ››  Import SSL Certificates and Keys**

| Import Type       | Key         | 
| -----------       | ----------- | 
| Key Name          |  apache.key |  
| Key Source        |  apache.key | 
| Security Type     |  Normal     | 

![Image](/img/apachekey.png)

| Import Type        | Certificate | 
| -----------        | ----------- | 
| Certificate Name   |  apache-certificate |  
| Certificate Source |  apache-certficate | 

![Image](/img/apache-certificate.png)

- **Task 2 : Create Server Side SSL Profile Like Below**

Navigate to **Local Traffic >> Profiles >> SSL >> Server**

| Name               | server-side-ssl-profile | 
| -----------        | -----------             | 
| Parent Profile     |  serverssl              |  
| Certificate        |  apache-certficate      | 
| Key                |  apache.key             |

![Image](/img/server-side-ssl.png)

- **Task 3 : Create Client Side SSL Profile Like Below**

Navigate to **Local Traffic >> Profiles >> SSL >> Client**


| Name                         | client-side-ssl-profile | 
| -----------                  | -----------             | 
| Parent Profile               |  clientssl              |  
| Certificate Key Chain        |  apache-certficate and apache.key      | 



![Image](/img/client-side-ssl-profile.png)

![Image](/img/client-ssl.png)

- **Task 4 : Create an HTTPS Pool Monitor like below**

| Monitor Name      | wiki.mon | 
| -----------       | ----------- | 
| Type              |  HTTPS       |  
| Send String       |  GET \r\n   | 
| Receive String    |  SERVER     |

![Image](/img/HTTPS-MON.png)

- **Task 5 : Create an HTTPS Pool like below**

| Pool Name         | wiki.pool | 
| -----------       | -----------  | 
| Health Monitors   |  wiki.mon |  
| Pool Members      |  172.16.20.1:443 , 172.16.20.2:443 , 172.16.20.3:443 |

![Image](/img/wikipool.png)


- **Task 6 :Create an Https Virtual Server Like Below**

| Virtual Server Name        | wiki.vs                  | 
| -----------                | -----------              | 
| Type                       |  Standart                |   
| Destination Address / Mask |  10.10.1.101             | 
| Server Port                |  443                     | 
| Protocol                   |  tcp                     |
| http profile               |  http                    |
| ssl profile (client)       |  client-side-ssl-profile |
| http profile               |  server-side-ssl-profile |
| default pool               |  wiki.pool               |

![Image](/img/wikivs1.png)
![Image](/img/wikivs2.png)
![Image](/img/wikivs3.png)

#### **Test And Results**

- Navigate to **Local Traffic >> Virtual Server** and note the status of the virtual servers : It is green

![Image](/img/wikivsstatus.png)

- Using windows client pc , using any browserser connect the https://10.10.1.101 virtual server and refresh the page 10 times.

- Navigate to **Local Traffic >> Pools >> Statistics** to monitor connections on each pool member.
  - How many connections to 172.16.20.1:443
  - How many connections to 172.16.20.2:443
  - How many connections to 172.16.20.3:443

![Image](/img/wikiconenctions.png)

- What is the status of the pool and pool members ? : Avaialble (green)

![Image](/img/wikipoolstatus.png)

![Image](/img/pool-members-status.png)

