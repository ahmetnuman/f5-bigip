---
layout: post
tags: http load baalncing
title: http load balancing
categories: f5-apm
---

## Lab 3.2 HTTP Load Balancing

- **Task 1 :Create a Pool Monitor Like Below**  

| Monitor Name      | wiki-80.mon | 
| -----------       | ----------- | 
| Type              |  HTTP       |  
| Send String       |  GET \r\n   | 
| Receive String    |  SERVER     | 

![Image](/img/monitor.png)

- **Task 2 :Create an Http Pool Like Below**  

| Pool Name         | wiki-80.pool | 
| -----------       | -----------  | 
| Health Monitors   |  wiki-80.mon |  
| Pool Members      |  172.16.20.1:80 , 172.16.20.2:80 , 172.16.20.3:80 | 

![Image](/img/wiki-pool.png)

- **Task 3 :Create an Http Virtual Server Like Below**

| Virtual Server Name        | wiki-80.vs         | 
| -----------                | -----------        | 
| Type                       |  Standart          |  
| Destination Address / Mask |  10.10.1.101   | 
| Server Port                |  80                | 
| Protocol                   |  tcp               |
| http profile               |  http              |
| default pool               |  wiki-80.pool      |

![Image](/img/wiki-vs1.png)

![Image](/img/wiki-vs2.png)


#### **Test And Results**

- Navigate to **Local Traffic >> Virtual Server** and note the status of the virtual servers : It is green

![Image](/img/wiki-vs2.png)

- Using windows client pc , using any browserser connect the http://10.10.1.101 virtual server and refresh the page 10 times.

- Navigate to **Local Traffic >> Pools >> Statistics** to monitor connections on each pool member.
  - How many connections to 172.16.20.1:80
  - How many connections to 172.16.20.2:80
  - How many connections to 172.16.20.3:80

![Image](/img/conenction-counts.png)

- What is the status of the pool and pool members ? : Avaialble (green)

![Image](/img/pool-status.png)

![Image](/img/member-status.png)
