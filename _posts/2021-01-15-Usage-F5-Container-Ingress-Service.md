---
layout: post
categories: cis
---

## Lab 3.2 F5 Container Connector Kullanımı

> Ahmet Numan Aytemiz, 13 Ocak 2021, Saat:03:07

---

#### App Deployment

#### 1. **kube-master üzerinde;** 2 replika f5-hello-world uygulaması oluştur.

- **deployment-hello-world.yaml** adındna bir dosya oluştur.
- Dosya içerisine aşağıdaki bilgileri yapıştır.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: f5-hello-world-web
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: f5-hello-world-web
  template:
    metadata:
      labels:
        app: f5-hello-world-web
    spec:
      containers:
      - env:
        - name: service_name
          value: f5-hello-world-web
        image: f5devcentral/f5-hello-world:latest
        imagePullPolicy: IfNotPresent
        name: f5-hello-world-web
        ports:
        - containerPort: 8080
          protocol: TCP


```

#### 2. nodeport-service-hello-world.yaml dosyası oluştur.

**kube-master** üzerinde **nodeport-service-hello-world.yaml** dosyası oluştur ve aşağıdaki bilgileri kopyala.

```
apiVersion: v1
kind: Service
metadata:
  name: f5-hello-world-web
  namespace: default
  labels:
    app: f5-hello-world-web
    cis.f5.com/as3-tenant: AS3
    cis.f5.com/as3-app: A1
    cis.f5.com/as3-pool: web_pool
spec:
  ports:
  - name: f5-hello-world-web
    port: 8080
    protocol: TCP
    targetPort: 8080
  type: NodePort
  selector:
    app: f5-hello-world-web

```

#### 3. ingress-hello-world.yaml dosyası oluştur 

**kube-master** üzerinde **ingress-hello-world.yaml** dosyası oluştur ve aşağıdaki bilgileri içine kopyala

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: f5-hello-world-web
  namespace: default
  annotations:
    virtual-server.f5.com/partition: "kubernetes"
    virtual-server.f5.com/ip: 10.1.10.101
    virtual-server.f5.com/http-port: "80"
    virtual-server.f5.com/ssl-redirect: "false"
    virtual-server.f5.com/balance: "round-robin"
    virtual-server.f5.com/health: |
      [
        {
          "path":     "f5.hello.world/",
          "send":     "HTTP GET /",
          "interval": 5,
          "timeout":  10
        }
      ]
spec:
  backend:
    serviceName: f5-hello-world-web
    servicePort: 8080


```

#### 4. Uygulamayı Başlat

```
kubectl create -f deployment-hello-world.yaml
kubectl create -f nodeport-service-hello-world.yaml
kubectl create -f ingress-hello-world.yaml

```

#### 5. Uygulama Pod'larının Durumunu Kontrol Et


kubectl get pods -o wide

![Image](/img/pods.png)

`kubectl describe svc f5-hello-world`

![Image](/img/svc.png)

#### 6. F5 Üzerinde Kontrollerini Yap

**Kubernetes üzerinde oluşturulan bu application  F5 üzerine dinakik bir şekilde gelmiş olması gerek**

F5 üzerinde;

- 10.1.10.101 ip adresli ve 80 portundan hizmet veren bir virtual server, bunun arkasında,
- 10.1.10.21,22 ve 23 ip adreslerinin 30990 portunda koşan pool member 

create edilmiş olması gerekmketedir. Uygulamaya dış dünyadan http://10.1.10.101 şeklinde erişildiğinde F5 bunları round robin yöntemi ile kubernetes sunucularının 30990 portuna , kubernetes de kendi içinde bunları kendi içinde dinamik oluşan iptables'ile pod'lara iletecektir.

![Image](/img/app.png)

**vs**
![Image](/img/virtual_server.png)
**pool**
![Image](/img/virtual_server.png)
**kubernetes sunucularu üzerindeki iptables**
![Image](/img/iptables.png)


**F5'in dinamik bir şekilde çalışıp çalışmadığını test etmek için;**

- Uygulamayı scale et ve o şekilde test et

`kubectl scale --replicas=10 deployment/f5-hello-world-web -n default`

