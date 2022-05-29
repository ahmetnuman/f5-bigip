---
layout: post
tags: Allow Only Supported Platforms
title: Allow Only Supported Platforms
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 27.05.2022 - Ankara, Turkey

---

## Lab 4.3 Allow Only Supported Platform

- **Task : Allow only windows 7 and windows 10 are allowed, other operating systems will drop**

  - Navigate to **Access >> Profiles/Policies : Access Profiles (Per-Session Polices)** and click **Copy** button for the policy named **wiki.ap.1** and Copied Profile Name **wiki.ap.4**

![Image](/img/copied-wiki-ap-4.png)


  - Click the **Edit** button for **wiki.ap.4** and create the following policy:

![Image](/img/supportedos.png)
![Image](/img/wiki-ap-4-macro.png)

  - Update the virtual server's access profile as **wik.ap.4** from **Local Traffic >> Virtual Server >> wik.vs**

![Image](/img/access-profile.png)

#### **Test And Results**

- **Connect https://10.10.1.101 vs address from linux client**

![Image](/img/linux-client.png)

- **Connect https://10.10.1.101 vs address from linux client**

![Image](/img/windows-client.png.png)

- Change the user agent string to Android and connect again the https://10.10.1.101 from windows client.

  
---
  