---
layout: post
title: Docker Installation
tags: Docker Installation
categories: docker
---

## Docker Kurulumu 

> Ahmet Numan Aytemiz, 13 Ocak 2021

---

#### Lab Machines

| Hostname    | Ip-Address                              | OS/Version          | 
| ------      | ---                                     | -----               |  
| bigip1      | 10.1.10.60 (Self IP),10.1.1.245 mgmt ip | tmos 13.1.3.1       |
| kube-master | 10.1.10.21                              | ubuntu server 16.04 |
| kube-node1  | 10.1.10.22                              | ubuntu server 16.04 |
| kube-node2  | 10.1.10.23                              | ubuntu server 16.04 |

## Lab 1.1 Install Docker

Docker Kurulumu Her 3 makine üzerinde (kube-master, kube-node1 ve kube-node2) makinaları üzerinde de yapılacaktır. Kurulumlar root kullanısı ile yapılacaktır

#### 1. Makineleri Update Et 

`apt update && apt upgrade -y`

#### 2. Makinelere Docker Reposu Ekle

`curl \-fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add \-`
`add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

#### 3. Docker Install Et

`apt update && apt install docker-ce -y`

#### 4. Docker'ın Çalışıp Çalışmadığını Test Et

`docker run --rm hello-world`

Herşey doğru kurulmuş ise aşağıdaki sonucu almamız gerek 

![Image](/img/docker-run.png)

## Lab 1.2 Docker Üzerinde Container Çalıştır

#### 1.Docker üzerinde test amaçlı myapache isminde httpd apache servisi çalıştır.

`docker run --rm --name "myapache" -d -it -P httpd:latest`

#### 2. Servisin Çalışıp Çalışmadığını Kontrol Et

`docker ps -f name=myapache`

![Image](/img/httpd.png)

Artık dış dünyadan 49153 portu üzerindne http://10.1.10.21:49153 şeklinde http servisine bağlanabiliriz.

![Image](/img/success1.png)

