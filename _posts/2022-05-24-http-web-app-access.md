---
layout: post
tags: HTTP Web Application Access 
title: HTTP Web Application Access 
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 24.05.2022 - Ankara, Turkey

---

## Lab 3.5 HTTP Web Application Access

- **Task 1 : Change the Access Profile like below**
   - Navigate to **Access >> Profiles/Polices : Access Profiles (Per-Session-Policies)** and click the link for the policy name **wiki.ap.1**
   - Click the **SSO / Auth Domains**
   - Disable the **Secure Cookie Option**, otherwise you will be able to use session cookies with non-SSL HTTP access.
   - Click **Update**

![Image](/img/disable-secure-cookie.png)

- **Task 2: Configure HTTP virtual server like below**

| Virtual Server Name        | wiki-80.vs         | 
| -----------                | -----------        | 
| Type                       |  Standart          |  
| Destination Address / Mask |  10.10.1.101       | 
| Server Port                |  80                | 
| Protocol                   |  tcp               |
| http profile               |  http              |
| Access Policy              |  wiki.ap.1         |
| default pool               |  wiki-80.pool      |

![Image](/img/wikivsapp.png)
![Image](/img/wikivsapp2.png)
![Image](/img/wikivsapp3.png)
![Image](/img/wikivsapp4.png)

#### Test and Results

- Using any browser connect the https://10.10.1.101 virtual server and enter invalid credentials three or more times.
- When using invalid credentials, what happens the first time ?

![Image](/img/firsttime.png)

- What happens the third time ?

![Image](/img/thirdtime.png)

- Connect to the https://10.10.1.101 virtual server log in using domain user credentials and refresh the page 10 times.
- What is the virtual server status (**Local Traffic >> Virtual Server**)
- Navigate to **Local Traffic >> Pools >> Statistics** to monitor connections on each pool member in the **wiki.pool**
  - How many connections to 172.16.20.1:443 ? **4**
  - How many connections to 172.16.20.2:443 ? **3**
  - How many connections to 172.16.20.3:443 ? **3**

![Image](/img/conenctionsstats.png)


- Enable Secure Cookie options and reconnect the http://10.10.1.101 and see the result

![Image](/img/securecookieenable.png)

