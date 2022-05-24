---
layout: post
tags: Policy Import, Export, Copy and Delete 
title: Policy Import, Export, Copy and Delete  
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 24.05.2022 - Ankara, Turkey

---

## Lab 4.2 Policy Import, Export, Copy and Delete 

#### Export and Import and Access Policy

- **Task 1 Export wiki.ap.1 Policy**

Navigate to **Access >> Profiles/Polices: Access Profiles (Per-Session Polices) >> Export** 

![Image](/img/exportpolicy.png)

- **Task 2 Import Policy**

Navigate to **Access >> Profiles/Polices: Access Profiles (Per-Session Polices) >> Import**

| New Profile Name           | wiki.ap.2          | 
| -----------                | -----------        | 
| Config File Upload         |  profile_Common_wiki.ap.1.conf.tar.gz  |  
| Reuse Existing Objects |  Enabled   | 


![Image](/img/importpolicy.png)

![Image](/img/import-policy.png)

- **Task 3 : Update the virtual server**

Navigate to **Local Traffic >> Virtual Server** and click **wiki.vs**

| Access Profile           | wiki.ap.2          | 

![Image](/img/wikiap2.png)


#### Test and Result

| Connect to the virtual server and determine if the policy behaves in exactly the same way           |           | 
| -----------                | -----------        | 
| Did you have to Apply Access Policy         |  Yes  |  
| Does it behaves the same way ? |  Yes   | 







