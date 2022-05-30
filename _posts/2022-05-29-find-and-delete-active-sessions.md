---
layout: post
tags: Find and Delete Active Sessions
title: Find and Delete Active Sessions
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 29.05.2022 - Ankara, Turkey

---

## Lab 5.2 Find and Delete Active Sessions

- Using two different browser (chrome and firefox) connect to wiki.vs https://10.10.1.101

![Image](/img/connect.png)

- Navigate to **Access >> Overview : Active Sessions**

![Image](/img/active-sessions.png)

- Select users and **Kill Selected Sessions**. Then click **delete**.

![Image](/img/killselected.png)

![Image](/img/delete.png)

- Open a **Firefox** browser to **wiki.vs** but do not log on , look for the session, note the session id and try to kill session.

![Image](/img/logonagain.png)

**what was the session id ?**

![Image](/img/deleteagain.png)

- refresh the firefox browser again, what was the session reference number ?

![Image](/img/referencenumber.png)


## Use Command Line 

- Using two different browser connect the https://10.10.1.101 wiki.vs again, and use different logon name.

![Image](/img/login-two.png)

- Connect to big-ip with ssh and enter the following command `sessiondump --allkeys | grep -a last.username`

![Image](/img/sessiondumpallkeys.png)

- kill one or more of the active sessions using `sessiondump --delete <session-id>` or `sessiondum --delete all`

![Image](/img/deletesession.png)



- Open a session to wiki.vs but do not logon , look for the session , we wont see a username (because we didnt enter a username)

`sessiondump --list`

![Image](/img/sessiondumplist.png)

