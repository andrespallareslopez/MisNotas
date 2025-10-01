---
Titulo: "Apuntes Kubernetes"
---

# Apuntes KuberneteS

### Helm, el gestor de paquetes para Kubernetes

https://www.youtube.com/watch?v=5-Qcig2_8xo



~~~
kubectl get nodes

kubectl get all

help repo add bitnami https://charts.bitnami.com/bitnami

helm install my-release bitnami/wordpress

helm show values bitnami/wordpress

helm install miwordpress bitnami/wordpress --wordpressUserName=admin --wordpressPassword=1234

# o poner la configuracion en un fichero de configuracion ymal, en vez de la linea de comandos

por ejemplo install.yml

helm install miwordpress -f install.yml bitnami/wordpress

#creacion de paquetos o chart
# crea una carpetas con ficheros yml para configurar el paquete o chart que vamos a crear.

helm create miapping

Chart.yml

values.yml






~~~




### Kubernetes Tutorial for Beginners [FULL COURSE in 4 Hours]

https://www.youtube.com/watch?v=X48VuDVv0do



- Componentes de kubernetes
----------------------------
* Pod (multiple container in one Pod)
* Virtual Networks (Each Pod gets its own IP address)
* Service - Permanent Ip address
    .The replica is connected to the same Service
    .Service has 2 functionalities: Permenent ip  and load balancer

* Ingress: which is used to route traffic
* Config Map - External configuration of your application
* Secret - used to store secret data like credentials, base64 encoded
  use it as variable environmets Secret
* Volumes: Storage on local machine or remote, outside of the k8s 
  .Storage its outside of k8s cluster
* Deployment: 
    .Databases We can`t be replicated via deployment! 
    .database has state
    .
* StatefulSet: for STATEFIL apps
    .its dificult and tedius work with statefulset.
    .its common practice to host database application outside of k8s cluster
    .DB are often hosted outside of K8s cluster.

* 

- Main Kubernetes Components summarized
----------------------------------------

* abstraction of conainers: Pos Service

* communication : Ingress 

* route traffic into cluster:

* External configuration: ConfigMap, Secrets, Volumes

* Deployment
* StatefulSet : Databases

- Basic Kubernetes Architecture
-------------------------------

* Thwo type of nodes
* Master, and Slaves

* Worker servers or nodes

* each node has multiple Pods on it

* 3 processes must be installed on every node.

* Worker Nodes do the actual work
* container runtime : its needs to be installed on every node 
* kubelet: its a process of kubernetes that interacts with both - the container and node
     .its responbile to take configuration and actually running a pod or starting a pod with a container inside  and then assigning resources from that node to the container like CPU RAM and storage resources
* Comunication via services: 
* Anotther process is kube Proxy forwards the request

Summaryce:
----------

* 3 node processes: 
  1. Kubelet
  2. Kube Proxy
  3. Container runtime

How do you interact with this cluster?

How to:
    Schedule pod?
    monitor, watching? if a pod die
    re-schedule/re-start Pod?
    join a new node?

All this things are done by Master nodes

* Managing processes are done by Master Nodes

* Master Processes

* 4 processes run on every master node

client update query master node across api server

1. Api server: client interact with Api server
    .cluster gateway
    .acts as a getekeeper for authentication
    .clients do some request to API server and its validates request and do other processses...
    .one entry point for reason security

2. scheluder:
     .schedule new Pod like start pod under condition
     .Where to put the pod?
     .kubelet

3. Controller manager
     .detects cluster state changes
4. etcd 
     .etcd is the cluster brain
     .cluster changes get stored in the key value store
     .what resources are available?
     .Did the cluster state changes?
     .aplication data is not stored in etcd


- Example Cluster Set-up

* Add new Master/Node server:

1. get new base server
2. install all the master/worker node processes
3. add it to the cluster


- Minikube and kubectl. Local setup

* Production cluster Setup
  .Multiple Master and worker nodes
  



~~~

~~~


(Win 10)
Podemos bajar nuestro instable de kubernetes minikube en el directorio Minikube_home para ejecutar y levantar kubertes.
Si es la primera vez dentro de este directorio se bajar archivos y establecera cosas.


En nuestra maquina local cuando instalemos kubernetes(minikube) tenemos que establecer la variable de entorno de MINIKUBE_HOME
 a disco c: porque si lo hacemos a otra unidad D: o E: vamos a tener problemas 

El ejecutable de minikube tambien nos lo podemos bajar y ponerlo en un directorio espeficico y registrar dicho direcctorio en variables de entorno.

**How to set up Kubernetes on Windows 10 with Docker for Windows and run ASP.NET Core**


https://www.hanselman.com/blog/HowToSetUpKubernetesOnWindows10WithDockerForWindowsAndRunASPNETCore.aspx

**04. Deploying into local Kubernetes in Windows 10 and Docker for Windows development environment**

https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-Deploying-into-local-Kubernetes-in-Windows-10-and-Docker-for-Windows-development-environment

**Getting Started With Kubernetes On Windows 10 Using HyperV And MiniKube**

https://www.c-sharpcorner.com/article/getting-started-with-kubernetes-on-windows-10-using-hyperv-and-minikube/

**Minikube on Windows 10 with Hyper-V(importante)**

En este articulo nos muestra como instalar y arrancar minikube en linea de comandos con hyperv

https://medium.com/@JockDaRock/minikube-on-windows-10-with-hyper-v-6ef0f4dc158c


**Arrancar un minikube**

~~~
minikube start --vm-driver="hyperv"

minikube start --vm-driver=hyperv --hyperv-virtual-switch="primaryswitch"
~~~

Con este comando creara un directorio a partir de la variable de entorno que hemos definido, si es la primera vez se bajara una imagen y
definira cosas.

Como decimos a principio de este documento tenemos que hacer todo esto en c:


**Comprobar minikubes**

~~~
minikubes status
~~~
Informacion del cluster
~~~
kubectl cluster-info
~~~

Parar un cluster

~~~
minikube stop
~~~

Si esta instruccion no funcionara meterse dentro de hyperv y dentro del cluster autentificarse como root
y poner *poweroff*

Como mostrarnos todos los addons activos en un cluster:

~~~
minikube addons list
~~~
Como mostrarnos el dashboard en navegador

~~~
minikube dashboard
~~~
____
Mostrar logs de kubernetes de un pod
~~~
kubectl log nginx(<-nombre del contenedor creado en kubernetes)
~~~


Putting the ".NET" into "Kubernetes"

https://www.youtube.com/watch?v=GBOPBfcJ2zM

Kubectl basics for beginners | Kubernetes

https://www.youtube.com/watch?v=feLpGydQVio&list=RDCMUCFe9-V_rN9nLqVNiI8Yof3w&index=12



~~~

~~~



____
.NET Microservices – Full Course (Les Jackson)

Les Jackson

https://www.youtube.com/watch?v=DgVjEo3OGBI&t=5s

es un curso muy largo pero interviene el despliegue y manejo de kubernetes para .net













