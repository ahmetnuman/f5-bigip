---
layout: post
tags: Provisionig the BIG-IP System and Confirm Network Configuration
title: Provisionig the BIG-IP System and Confirm Network Configuration
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 18.05.2022 - Ankara, Turkey

---

#### 1. Provision Big-IP System

Navigate `System > Resource` and provision like Big-IP modules like below ;

- Local Traffic (LTM) : Nominal
- Access Policy (APM) : Nominal
- Management : Small

![Image](/img/resource-provision.png)

After resource porovisioning big-ip system will reboot.

#### 2. Configure NTP and DNS on the F5-APM

To configure NTP navigate **System > Configuration >> Device >> NTP**  and add the 172.16.20.20 ip address to the server list according to topology then update.

![Image](/img/f5-ntp.png)

To configure NTP navigate **System > Configuration >> Device >> DNS**  and add the 172.16.20.20 ip address to the dns lookup server list and add f5apm.lab to the dns search domain list according to topology then update.

![Image](/img/f5-dns.png)

#### 3. Configure Vlans

Configure the vlan according to topology like below ;

| Vlan Name      | Tag         | Untagged Interfaces | Partitions  |
| -----------    | ----------- | -----------         | ----------- |
| External       |  4093       |  1.1                | Common      |
| internal       |  4094       | 1.2                 | Common      |

To configure vlan navigate **Network >> VLANs >> Vlan List >> Create **

- External Vlan

![Image](/img/external-vlan.png)

- Internal Vlan

![Image](/img/internal-vlan.png)

#### 4. Configure Self and Floating IP 

Configure the self and floating ip adresses according to topology like below ;

| Name                 | Ip Address      | Netmask          | Vlan         | Traffic Group            | Port Lockdown |
| ---------            | ---------       | -----------      | -----------  | -----------              | -----------   |
| external-self        | 10.10.1.31      | 255.255.255.0    |  external    | traffic-group-local-only | 443 and 22    | 
| external-floating    | 10.10.1.33      | 255.255.255.0    |  external    | traffic-group-1          | 443 and 22    |
| internal-self        | 172.16.1.31     | 255.255.255.0    |  internal    | traffic-group-local-only | default       | 
| internal-floating    | 172.16.1.33     | 255.255.255.0    |  internal    | traffic-group-1          | default       | 

To configure the self and floating ips navigate **Network >> Self IPs ** >> **Create**

- Configure external-self ip address

![Image](/img/external-self.png)

- Configure external-floating ip address

![Image](/img/external-floating.png)

- Configure internal-self ip address

![Image](/img/internal-self.png)

- Configure internal-floating ip address

![Image](/img/internal-floating.png)

#### 5. Configure big-ip's hostname

To configure the hostname navigate **System >> Platform**

![Image](/img/bigip-hostname.png)

#### 6. Create a UCS Archive of Configuration

Navigate **System >> Archives** and back up current system's configuration.

![Image](/img/backup-apm.png)

--------