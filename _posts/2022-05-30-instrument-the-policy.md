---
layout: post
tags: Instrument the Policy
title: Instrument the Policy
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 30.05.2022 - Ankara, Turkey

---

## Lab 5.4 Instrument the Policy

**The Message Box Agent is often used to debug an Access Policy. It acts to pause the policy at a specisifc point. Session variables may be inspected to determine the state of teh policy while it is paused**

- **Tasks: Copy wiki.ap.1 and new name will be wiki.ap.6**

![Image](/img/wikiap6.png)

- **Edit wiki.ap.6 like below**

![Image](/img/messagebox.png)

- **Apply wiki.ap.6 to the wiki.vs virtual server**

![Image](/img/apwikvs6.png)

## Test and Result

- **Connect from browser to wiki.vs but do not logon. We will see the message telling us to click a link before continuing. Wait and do not click yet.**

![Image](/img/sessiondump1.png)

- On the command line enter the following command to save all of the current session variables.

```
mkdir /root/temp2
cd /root/temp2
sessiondump --allkeys > dump1.txt
```

![Image](/img/dump1.png)

- **In the browser click the link to continue**

- **We will see the logon page. Enter credentials**

- **We will see immediately see a second message telling us to click the link before continuing.**

![Image](/img/secondcontinue.png)


- **On the command line enter the following command to save all of the current session variables.**

`sessiondump --allkeys > dump2.txt`

![Image](/img/secondcontin.png)

- **In the browser click link to continue. You should now see the website**

![Image](/img/website.png)

- **On the command line enter the following command a final time**

`sessiondump --allkeys > dump3.txt`

![Image](/img/dump3txt.png)

## Inspect Where Session Variables are Created

- **On the command line execute the following commands**

```
wc -l dump1.txt
wc -l dump2.txt
wc -l dump3.txt
```

![Image](/img/wcldump.png)

- **We should notice the number of lines increases with each dump.**

- **On the command line, run the follwing command to view the session variables in the first file**

`less dump1.txt`

![Image](/img/lessdump1.png)

- **Now look at the variables added at the second capture point in the policy**

`diff -a dump1.txt dump2.txt`

![Image](/img/diffdumps.png)

- **Now look at the variables added at the third capture poıint in the policy**

![Image](/img/diffdumpsthird.png)


