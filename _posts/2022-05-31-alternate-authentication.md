---
layout: post
tags: Alternate Authentication
title: Alternate Authentication
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 31.05.2022 - Ankara, Turkey

---

## Lab 6.2 Alternate Authentication

**Tasks**

- Create a second authentication server. Navigate to **Access >> Authentication : RADIUS** and click **Create** 

| AAA Server Name            | radius.aaa         | 
| -----------                | -----------        | 
| Type                       |  radius            |  
| Mode                       |  Authentication    | 
| Server Connection          |  Direct            | 
| Server address             |  172.16.20.21      |
| Port                       |  1812              |
| Secret                     |  f5apm             |

![Image](/img/radiusadddirect.png)


- Create an Access Profile named wiki.ap.7 and edit the Access Policy Like below.

![Image](/img/radiusap.png)

- Change the wiki.vs virtual server to use this policy.

![Image](/img/wikiap7.png)

- Connect the https://10.10.1.101 wiki.vs from the windows client and test the radius server.

![Image](/img/anumanradius.png)

![Image](/img/authradius.png)

- Edit the **wiki.ap.7** policy like the following (Ax Logon Attempts Allowed 1 both radius and ad auth)

![Image](/img/wikap7-new.png)

After the change access policy test the users.