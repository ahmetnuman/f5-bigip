---
layout: post
tags: Use a Logging Agent
title: use a Logging Agent
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 30.05.2022 - Ankara, Turkey

---

## Lab 5.1 Use a Logging Agent

**Session variables are purged from memory as soon as the session is terminated, but sometimes it would be useful to save some of those variables for inspection hours or days after the session was finished.**

- **Tasks: Copy wiki.ap.1 policy from Access >> Profiles/Policies : Access Profiles (Per Session Policies) and name it wiki.ap.5**

![Image](/img/copy-wiki-ap-5.png)

- Edit **wiki.ap.5** like below and Click the **Apply Access Policy**:

![Image](/img/logging.png)

- Update the Virtual Server Access profile , apply the wiki.ap.5

![Image](/img/wikivsapply.png)

## Test and Results

- Connect the https://10.10.1.101 wiki.vs and logon. 

![Image](/img/connectwikis.png)

- Examine logs with `less /var/log/apm` or `tail -n 15 /var/log/apm` commands.

![Image](/img/varlogapm.png)


