---
layout: post
tags: Web Application Access 2
title: Web Application Access 2
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 23.05.2022 - Ankara, Turkey

---

## Lab 3.4 Web Application Access 2


- **Task 1 : Create an Active Directory AAA Server Like Below**

Navigate to **Access >> Authentication >> Active Directory** and click **Cretae**

| AAA Server Name       | f5apm.lab         | 
| -----------           | -----------       | 
| Type                  |  Active Directory |  
| Domain Name           |  f5apm.lab        | 
| Server Connection     |  Direct           | 

![Image](/img/f5aaa.png)

- **Task 2 : Create an Access Profile**

Navigate to **Access >> Profiles/Polices: Access Profiles (Per Session Policies)** and click **Create**

| Access Profile Name   | wiki.ap.1   | 
| -----------           | ----------- | 
| Profile Type          |  All        |     
| Language              |  English    |

![Image](/img/wiki-ap1.png)

- **Task 3 : Edit new Access Policy (wiki.ap.1)**

Navigate to **Access >> Profiles/Policies : Access Profiles (and) click Edit on the same line as wiki.ap.1**

Edit your policy like below and in the AD Auth choose **Server:/Common/f5apm.lab**

![Image](/img/access-policy.png)

And click **Apply Access Policy**


- **Task 4: Edit HTTPS Virtual Server to add Access Policy like below**

| Virtual Server Name        | wiki.vs                  | 
| -----------                | -----------              | 
| Type                       |  Standart                |   
| Destination Address / Mask |  10.10.1.101         | 
| Server Port                |  443                     | 
| Protocol                   |  tcp                     |
| http profile               |  http                    |
| ssl profile (client)       |  client-side-ssl-profile |
| http profile               |  server-side-ssl-profile |
| Access Profile             |  wiki.ap.1               |
| default pool               |  wiki.pool               |

![Image](/img/wikivsap.png)
![Image](/img/wikivsap1.png)
![Image](/img/wikivsap2.png)
![Image](/img/wikivsap3.png)

#### Test and Results

- Using any browser connect the https://10.10.1.101 virtual server and enter invalid credentials three or more times.
- When using invalid credentials, what happens the first time ?

![Image](/img/wronguser.png)

![Image](/img/wronguser2.png)

- What happens the third time ?

![Image](/img/wronguser3.png)

- Connect to the https://10.10.1.101 virtual server log in using domain user credentials and refresh the page 10 times.
- What is the virtual server status (**Local Traffic >> Virtual Server**)
- Navigate to **Local Traffic >> Pools >> Statistics** to monitor connections on each pool member in the **wiki.pool**
  - How many connections to 172.16.20.1:443 ? **0**
  - How many connections to 172.16.20.2:443 ? **10**
  - How many connections to 172.16.20.3:443 ? **0**

![Image](/img/connectionsuser.png)

- Open new tab with same browser and analyze the connection numbers on the pool members again.

![Image](/img/conenctionsagain.png)


