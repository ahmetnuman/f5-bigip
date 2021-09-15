---
layout: post
tags: Installing Kubernetes Cluster
title: Installing Kubernetes Cluster
categories: kubernetes
---

## Lab Setup 

> Ahmet Numan Aytemiz, 13 Ocak 2021

---

#### Lab Machines

| Hostname    | Ip-Address                              | OS/Version          | 
| ------      | ---                                     | -----               |  
| bigip1      | 10.1.10.60 (Self IP),10.1.1.245 mgmt ip | tmos 13.1.3.1       |
| kube-master | 10.1.10.21                              | ubuntu server 16.04 |
| kube-node1  | 10.1.10.22                              | ubuntu server 16.04 |
| kube-node2  | 10.1.10.23                              | ubuntu server 16.04 |

## Lab 2.1 Ubuntu Sunucları Kubernetes Kurulumuna Hazırla

**Aşağıdaki işlemleri her 3 sunucu üzerinde yap

#### 1. Sunucuların /etc/hosts kaydına birbirlerini ekle

```
10.1.10.21 kube-master
10.1.10.22 kube-node1
10.1.10.23 kube-node2
```

#### 2. Linux Swap dosyasını disable et

`swapoff -a` 

**/etc/fstab dizini altında bulunan**

 - `UUID=b74b0588-ce84-41c6-8159-3842e691ee5f none            swap    sw              0       0
`
satırının başına **#** ekle, burayı yoruma çek

#### 2. Sunucuları update et

`apt update && apt upgrade -y`

#### 3. Her Sunucuya Docker Yükle

**Birinci lab'da bu adım zaten yapılmıştı.

#### 4. Docker cgroupdrive Konfigurasyonu 

```
cat << EOF > /etc/docker/daemon.json
{
"exec-opts": ["native.cgroupdriver=cgroupfs"]
}
EOF
```

#### 5. Kubernetes reposunu sunuculara ekle

```
cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

#### 6. Sunucular üzerine kubernetes'i kur.

`apt update && apt install kubelet kubeadm kubectl -y`

## Lab 2.2 Master Kurulumu 

Master tüm kubernetes sisteminin yönetimini yapar. Aşağıdaki komutları sadece kube-master node'u üzerinde yapıyoruz.

#### 1. Kubernetes'i Başlat

`kubeadm init --apiserver-advertise-address=10.1.10.21 --pod-network-cidr=10.244.0.0/16`

Bu işlemi yaptıktan sonra **Your Kubernetes control-plane has initialized successfully!** uyarısı almış olmamız lazım, yoksa bi sıkıntı var demektir.

**kubeadm join 10.1.10.21:6443 --token ictquv.5ghdbl830ae1ci9x --discovery-token-ca-cert-hash sha256:5b6c96bdaf47832efeef668985e27bca832f149bbd59c6cacb74f5b9f99203d3** satırını bir dosyaya kaydetmeyi unutma, bunu node'ları master'a dahil ederken kullancağız

#### 2. Kubernetese admininitration konfigurasyonu

**root kullanıcısı için;**

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

**sistem üzerindeki normal kullanıcı için**

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

```

bu işlemleri ayrı ayrı yap.

#### 3. Kubernetes'in up ve running olduğunu kontrol et

`kubectl get pods --all-namespaces`

![Image](/img/kube-master.png)

#### 4. flannel'ı yükle

`kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml`

#### 5. kubernetes servislerini tekrar konrol et

`kubectl get pods --all-namespaces`

**tekrar kontrol ettiğinde tüm servilerin running durumda olması gerek**

![Image](/img/running.png)

#### 6. Ek olarak kubernetes durumunu tekrar kontrol et

`kubectl get cs`


`kubectl cluster-info`

![Image](/img/clusterinfo.png)

## Lab 2.3 Node Kurulumu

#### 1. Node'ları master'a join et. 

**Bu komutu kube-node1 ve kube-node2 üzerinde çalıştır.**

``kubeadm join 10.1.10.21:6443 --token w07sez.7gq4ccdzcmpl6o22 --discovery-token-ca-cert-hash sha256:7c0cc4e4900f103a2003c9ea3d6aba7411fc206d496760dd7e77122242a67c20`` 

![Image](/img/join.png)

#### 2. Node'ların Cluster'a Başarılı Bir şekilde join olduğunu kontrol et

**Bu komutu kube-master üzerinde çalıştır.**

`kubectl get nodes`

![Image](/img/get_nodes.png)


#### 3. Master Üzerinde Servislerin Runnig Durumda Olup Olmadığını Kontrol Et

`kubectl get pods --all-namespaces`

![Image](/img/services.png)

## Lab 2.4 Kubernetes UI Kurulumu

**Aşağıdaki komutları kube-master üzerinde çalıştırıyoruz**

#### 1. Install Kubernetes UI

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.1.0/aio/deploy/recommended.yaml`

#### 2. Konfigure UI

`kubectl create serviceaccount kubernetes-dashboard -n kube-system`

` kubectl create clusterrolebinding dashboard-admin -n default  --clusterrole=cluster-admin  --serviceaccount=default:dashboard`

`kubectl port-forward -n kubernetes-dashboard service/kubernetes-dashboard 8080:443 --address='0.0.0.0'`

#### 3. Web UI'a bağlanmak için Token Al 

` kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode`

![Image](/img/token.png)

`https://10.1.10.21:8080` ile UI'a token ile bağlan

![Image](/img/webui.png)

**Cluter>>Nodes** kısmında altında cluster içindeki nodeları görebiliriz.

![Image](/img/nodes.png)

