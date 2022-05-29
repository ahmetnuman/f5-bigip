---
layout: post
tags: Managing Big-IP APM Notes
title: Managing Big-IP APM Notes
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 29.05.2022 - Ankara, Turkey

---

#### Big-IP APM Sessions and Access Licenses

When a connection is made to a virtual server with an Access Policy , BIG-IP APM automatically assigns a session id to that connection and tracks it with a session cookie and in the session database which uses memcache. 

Every Big-IP system has a specific maximum of session it can support.

#### Session Variables and sessiondump

The sessiondump command is a tool will help us understand Big-IP APM sessions. A session is made up potentially hundereds of session variables that describe the session. Sessiondump display these variables.

`sessiondump -allkeys` command display every session variable entry in the Access Policy memcache.

`sessiondump --allkeys | grep 'session\.logon\.last\.username'` command will dump all the current users on BGG-IP APM.

`sessiondump --allkeys | grep 'last\.username\|user\.agent'` this command will list which user is connecting which user agent.

`sessiondump --allkeys | grep 'lat\.username.* ann$'` this commadn is used to search for a specisic user.

`sessiondum --sid 03b621f6 | wc -l`

`sessiondump --delete 03b621f6`

`sessiondum --sid 03b621f6 | wc -l`

We can also view users with navigate to **Access > Overview > Active Sessions** from the Gui.
