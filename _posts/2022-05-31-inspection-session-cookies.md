---
layout: post
tags: Inspect Session Cookies
title: Inspect Session Cookies
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 31.05.2022 - Ankara, Turkey

---

## Lab 5.5 Inspect Session Cookies

**Session variables contain the data needed to manage a specific big-ip session and cookies contain the data needed to map specific browser session to big-ip sessions**

- **Tasks: Close every instance of Internet Explorer and open a new internet explorer window.**

- **Click Tools:F12 Developer Tools in the menu, then click network, then click green triangle to begin capturing traffic**

- **In the browser, connect to https://10.10.1.101 and logon**

- **Click DETAILS: Cookies and note the session cookie**

![Image](/img/displaycokkie.png)

## Test and Results 

- **What is the session id found in the cookie?** : 544e711f

