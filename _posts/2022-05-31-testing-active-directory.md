---
layout: post
tags: Testing Active Directory
title: Testing Active Directory
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 31.05.2022 - Ankara, Turkey

---

## Lab 6.1 Testing Active Directory

**We will briefly describe a few tools that can be used to inspect data stored on Active Directory. These tools can be used for troubleshooting. However, assuming connectivity is good and DNS is working correctly, the most common reason for an AD AutH and AD query to fail is clock skew greater than five minutes. In the lab, big-ip gets its clock setting using ntp directly the Active Directory server, so this should not be a problem**

- **Tasks**

- Connect to big-ip from cli.

- Type the following at the command prompt: `ping -c 4 172.16.20.20` This tests conenctivity to the Active Directory Controller. Expect a time of a few milliseconds for each response.

![Image](/img/pingad.png)

- Type the followind command : `nslookup -type=srv _ldap._tcp.f5apm.lab`

We should see an SRV record response that point to f5apm.lab. This is how Active Directory finds the domain controller when it is not expicitly configured.

![Image](/img/srvrecord.png)

- Type the following: `adtest -t auth -r f5apm.lab -u anuman -w Aa123456`

Use this command to confirm valid credentials. It also confirms that Active Directory AAA Server on big-ip is configured correctly.

![Image](/img/testaduser.png)

- Test again invalid credentials `adtest -t auth -r f5apm.lab -u anuman -w wrongpass`

![Image](/img/wrongpass.png)

- Type the following command to determine the group members of a user. `ldapsearch -x -D anuman -w Aa123456 -h f5apm.lab -b cn=anuman,cn=users,dc=f5apm,dc=lab memberOf`

![Image](/img/memberof.png)

- Determine the big-ip system's time and the NTP server's time using.

`date`
`ntpdate -q 172.16.20.20`

![Image](/img/datentp.png)


