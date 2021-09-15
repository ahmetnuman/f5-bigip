---
layout: post
categories: cis
---

## Lab 3.1 F5 Container Ingress Service Kurulumu

> Ahmet Numan Aytemiz, 15 Ocak 2021, Saat 03:07

---

**Bu lab'ı kurulumu yapabilmemiz için lisanlı F5 BIG-IP'YE ihtiyacımız var**

F5 e managmet ip adresi üzerinden bağlatı sağlıyoruz.

#### 1. F5 Üzerinde Container Connector Partition'ı Kur

Bunun için CLI'dan 

`tmsh create auth partition kubernetes`

Ya da Web Managemet üzerinden 

`System --> Users --> Partition List`
-  `Create ` `(ismi kuberbetes)`
-  `Click Finished`

![Image](/img/partition.png)

#### 2. F5 Üzerinde AS3 Servisini Eneble Et

- Bunun için önce Package Management LX (Eğer Big-IP versiyonu 14.0 dan önce ise) enable et,

`touch /var/config/rest/iapps/enable`

- https://github.com/F5Networks/f5-appsvcs-extension/releases adresindeki f5-appsvcs-3.25.0-3.noarch.rpm dosyasını local pc'ine download et.

- Sonra bu rpm dosyasını **iApps>Package Management LX > Import** ile import et

![Image](/img/rpm.png)

- Eğer doğru install etmiş ise **https://<mngmt-ip>/mgmt/shared/appsvcs/info** adresini aşağıdaki gibi cevap dönmesi gerek.

![Image](/img/response.png)

**Bu işlemleri F5 BIG-IP üzerinde yaptıktan sonra tekrar kube-master'a dön.**

#### 3. Nodeport Mode

**F5 login secret oluştur**

`kubectl create secret generic bigip-login -n kube-system --from-literal=username=admin --from-literal=password=admin`

**bigip Kontroller servis accoutu oluştur**

``
kubectl create serviceaccount k8s-bigip-ctlr -n kube-system
``

**servis accuntuna admin hakları ver**

``
kubectl create clusterrolebinding k8s-bigip-ctlr-clusteradmin --clusterrole=cluster-admin --serviceaccount=kube-system:k8s-bigip-ctlr
``


nodeport-deployment.yaml adında bir dosya kube-master üzerinde oluştur ve aşağıdaki bilgileri içine yapıştır.

```

apiVersion: apps/v1
kind: Deployment
metadata:
  name: k8s-bigip-ctlr
  namespace: kube-system
spec:
  replicas: 1
  selector:
    matchLabels:
      app: k8s-bigip-ctlr
  template:
    metadata:
      name: k8s-bigip-ctlr
      labels:
        app: k8s-bigip-ctlr
    spec:
      serviceAccountName: k8s-bigip-ctlr
      containers:
        - name: k8s-bigip-ctlr
          image: "f5networks/k8s-bigip-ctlr:2.1.1"
          imagePullPolicy: IfNotPresent
          env:
            - name: BIGIP_USERNAME
              valueFrom:
                secretKeyRef:
                  name: bigip-login
                  key: username
            - name: BIGIP_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: bigip-login
                  key: password
          command: ["/app/bin/k8s-bigip-ctlr"]
          args: [
            "--bigip-username=$(BIGIP_USERNAME)",
            "--bigip-password=$(BIGIP_PASSWORD)",
            "--bigip-url=https://10.1.10.60",
            "--insecure=true",
            "--bigip-partition=kubernetes",
            "--pool-member-type=nodeport"
          ]


```

#### 4. k8s-bigip-ctlr container'ını kubernetes üzerinde create et

`kubectl create -f nodeport-deployment.yaml`

#### 5. Kubernetes üzerinde deploy edilen k8s-bigip-ctlr container'ının durumunu kontrol et

`kubectl get deployment k8s-bigip-ctlr --namespace kube-system`

![Image](/img/ready.png)

#### 6. Oluşturulan k8s-bigip-ctlr container'ı hangi node üzerinde koşuyor bi bak

`kubectl get pods -o wide -n kube-system`

![Image](/img/control_node.png)

Görüldüğü üzere kube-node1 üzerinde koşmaya başladı.
