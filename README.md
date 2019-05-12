 **Project: “Cloud Computing in European schools”**  
<img src="/img/cloud-computing-logoproject.jpg" height="100" width="170"/>

 Number: Project: 2017-1-ES01-KA202-038471

<img src="/img/cofinanciadoEN.png" height="50" width="200"/> <img src="/img/logoIES-Modificado.png" height="75" width="200"/>  




# Introduction to PaaS: develop, deploy, run and manage apps on the Cloud  



#### Disclaimer
&nbsp;&nbsp;&nbsp;  *"The European Commission support for the production of this publication does not constitute an endorsement of the contents which reflects the views only of the authors, and the Commission cannot be held responsible for any use which may be made of the information contained therein."*




#### Author

&nbsp;&nbsp;&nbsp;  This material has been produced by Nico Fernández, Miguel Rodríguez, Alexis Ruiz under the Creative Commons licence:  <img src="/img/Licencia-Tipo2.png" height="25" width="75"/>  




### Objective
&nbsp;&nbsp;&nbsp; Platform as a Service (PaaS), is a cloud computing model that allows the users to develop, deploy, run and manage applications without taking care about the underlying layers. The alternatives used today focus on the use of containers which promote the **microservices based application** development approach (vs **monolithic applications**), because the different services into which we the application is separated can easily run in different containers. We will make a study of Docker, Kubernetes and OpenShift in order to develop, deploy, run and manage  microservices based applications.

&nbsp;&nbsp;&nbsp;This activity has been developed for developing the professional competence includes in the Erasmus+ project "Cloud Computing in European Schools".

</br>
</br>
</br>

# Docker Index:

**[Docker installation: virtual machine managed by Vagrant](#1).**

> **[1- Vagrant and Docker Installation](#2):**
>
> **[2- Docker applications lifecycle:](#3)**
>
> **[3- Docker containers: not persistent](#4):**
<br>
<br>
<br>

</br>
</br>
</br>

# Kubernetes Index:

**[KUBERNETES](#1k).**

> **[1- Introduction](#2k):**
>
> **[2- Installation & Start](#3k)**
>
> **[3- Working with minikube](#4k):**
<br>
<br>
<br>

<a name="1"></a>
# Docker installation: virtual machine managed by Vagrant.

The first step of our installation of docker is to have already installed the virtual machine manager called Vagrant. **But what is Vagrant?**

**Vagrant** is a tool for building and managing virtual machine environments in a single workflow. With an easy-to-use workflow and focus on automation, Vagrant lowers development environment setup time, increases production parity, and makes the "works on my machine" excuse a relic of the past. Machines are provisioned on top of VirtualBox, VMware, AWS, or any other provider.

The main commands for Vagrant are:

1.  **vagrant box add …** → download image / box from Vagrant repository. Example: vagrant box add ubuntu/bionic64 --provider virtualbox --\> download an image (box) of Ubuntu version Bionic 64 bits for VirtualBox.

2.  **vagrant box list** → list all downloaded images / boxes.

3.  **mkdir FOLDER** → create folder where we will create the Vagrantfile file that will contain the definition of the MV.

4.  **cd FOLDER** → go in inside the folder.

5.  **vagrant init BOX** → The MV files are located in the directory where the hypervisor (VirtualBox, VMWare ...) stores its MVs. In FOLDER, the VagrantFile file, a log file and a hidden .vagrant folder will be saved. Example: vagrant init ubuntu/bionic64 --\> the box used is ubuntu bionic 64.

6.  **vagrant up** → start the MV --\> We can check the virtual machine running by open the VirtualBox app.

7.  **vagrant ssh** → connect to the MV

8.  **vagrant halt** → stop the MV

So now you must be very concentrated to follow this steps:




</br>
</br>
</br>

<a name="2"></a>
# 1- Vagrant and Docker Installation: 

<span class="underline">1º Step:</span>

We must create a workspace for Vagrant where the configuration file of Vagrant is going to be there (Vagrantfile describes the type of machine , and how to configure and provision it).Then we are going to create a directory where we are going to “UP” the boxes(images ).

<p align="center"><img src="img/media/image1.png" height="150" width="600"/></p>

The Vagrantfile must be created in vagrant folder and must contains this configuration: (Upload Vagrantfile)

<p align="center"><img src="img/media/image2.png" style="width:4.96875in;height:4.02083in" /></p>

At the end of this file we can see how it is configured to install docker in the box that will be downloaded later

<img src="img/media/image3.png" style="width:6.87011in;height:2.28646in" />

<span class="underline">2º Step:</span>

> ***-- sudo apt install vagrant***

#### <p align="center"><img src="img/media/image4.png" style="width:4.71904in;height:1.80729in" /></p>

#### <span class="underline">3º Step:</span>

####  Install VirtualBox:

> ***-- sudo apt install virtualbox***

<p align="center"><img src="img/media/image5.png" style="width:6.27083in;height:1.13889in" /></p>

<span class="underline">4º Step:</span>

Get an image from Vagrant web:

> ***-- vagrant box add ubuntu/bionic64 --provider virtualbox***
<p align="center"><img src="img/media/image6.png" style="width:4.98958in;height:2.07292in" /></p>

*(This is the box (image) that it is going to be use as basis to install docker)*

<span class="underline">5º Step:</span>

Checking that everything has worked correctly:

> ***-- vagrant box list***

<p align="center"><img src="img/media/image7.png" style="width:6.27083in;height:1.51389in" /></p>

<span class="underline">6º Step:</span>

With the following command, the ubuntu box downloaded will be started applying the Vagrantfile configuration

> ***-- vagrant up***

<p align="center"><img src="img/media/image8.png"  width="600" style="height:0.83854in" /></p>

<span class="underline">7º Step</span>

Finally, we can access to the created box by ssh connection and check if docker is been successfully installed.

SSH connection:

> ***-- vagrant ssh***

<p align="center"><img src="img/media/image9.png" height="300" width="600"/></p>



</br>
</br>
</br>

<a name="3"></a>
# 2- Docker applications lifecycle:

After installing an environment with Docker, we are going to develop Docker images and deploy containers to run our applications.

<span class="underline">1º Step:</span>

First of all we are going to create a directory called “public\_html” and inside of it we need to create an other thing, a web page called “index.html”. It will be served by a web server that will run in a Docker container.

<p align="center"><img src="img/media/image10.png" style="width:6.24981in;height:0.94271in" /></p>

<span class="underline">2º Step:</span>

Now we need to create a docker image, but before doing that, we are going to create a Dockerfile in which define the following instructions that will be executed in the moment of building the docker image:

-   Update repositories and install Apache2

-   Clean and remove packages

-   Copy our webpage to the public directory of Apache (/var/www/html).

> Dockerfile must be created in the vagrant fold of /home

<p align="center"><img src="img/media/image11.png" style="width:6.29167in;height:1.66667in" /></p>

<span class="underline">3ºStep:</span>

Create the docker image. using the following command:

> ***-- docker build -t accountName/aplicacionesweb:v1***

<p align="center"><img src="img/media/image12.png" style="width:6.461in;height:0.93229in" /></p>

And use this command to see which images you have:

> ***-- docker image ls***

<p align="center"><img src="img/media/image13.png" style="width:6.34394in;height:0.88021in" /></p>

<span class="underline">4ºStep</span>

Upload our docker image to a repository in Dockerhub ([<span class="underline">hub.docker.com</span>](https://hub.docker.com/))

Log in our dockerhub account:

> ***-- docker login***

<p align="center"><img src="img/media/image14.png" style="width:6.07292in;height:1.0625in" /></p>

Upload the docker image to a repository in our account:

> ***-- docker push accountName/repositoryName:”imageName”***

<p align="center"><img src="img/media/image15.png" style="width:6.44329in;height:0.69271in" /></p>

<span class="underline">5ºStep</span>

<span class="underline"> </span>

<span class="underline"> </span> Download a docker image from dockerhub:

> ***-- docker pull accountName/repositoryName:”imageName”***

<p align="center"><img src="img/media/image16.png" style="width:6.44329in;height:0.69271in" /></p>

<span class="underline">6º Step</span>

Run a container from the downloaded image:

> **-- docker run --name “containerName” -d -p “ports” accountName/repositoryName:”imageName”**

<p align="center"><img src="img/media/image17.png" style="width:6.5in;height:0.3125in" /></p>

<span class="underline">7º Step</span>

Connect locally using links browser (text browser) and check the web page:

<p align="center"><img src="img/media/image18.png" style="width:4.60938in;height:0.41612in" /></p>

<p align="center"><img src="img/media/image19.png" style="width:6.75in;height:1.69792in" /></p>

<span class="underline">8º Step</span>

Modify the application:

<p align="center"><img src="img/media/image20.png" style="width:4.75521in;height:1.31985in" /></p>

For every new version we create, we need to follow this steps:

<span class="underline">8.1º Step</span>

Create the new image (in the development environment).

> ***-- docker build -t accountName/aplicacionweb:v2***

<p align="center"><img src="img/media/image21.png" style="width:6.55035in;height:1.78646in" /></p>

<span class="underline">8.2º Step</span>

Upload the new image.

> ***-- docker push accountName/aplicacionesweb:v2***

<p align="center"><img src="img/media/image22.png" style="width:6.30922in;height:0.53646in" /></p>

<span class="underline">8.3º Step</span>

Download the new image to the production environment.

> ***-- docker pull accountName/aplicacionesweb:v2***

<p align="center"><img src="img/media/image23.png" style="width:6.21875in;height:0.64583in" /></p>

<span class="underline">8.4º Step</span>

Delete the current container (in the production environment):

> ***-- docker container rm -f aplweb***

<p align="center"><img src="img/media/image24.png" style="width:6.27083in;height:1.18056in" /></p>

<span class="underline">8.5º Step</span>

Run the new container:

> ***-- docker run --name aplweb2 -d -p 80:80 accountName/aplicacionesweb:v2***

<p align="center"><img src="img/media/image25.png" style="width:6.21354in;height:1.70654in" /></p>


</br>
</br>
</br>

<a name="4"></a>
# 3- Docker containers: not persistent: 

This section explains the need to use persistent volumes due to data in containers are lost.

<span class="underline">1º Step:</span>

We are going to create a container with a MySQL server; the data is stored in a persistent volume.

> ***-- docker run --name some-mysql -v /opt/mysql:/var/lib/mysql -e MYSQL\_ROOT\_PASSWORD=asdasd -d mysql***

<img src="img/media/image26.png" style="width:6.0625in;height:1.5625in" />

<span class="underline">2º Step:</span>

Create a database called dbtest.

> ***-- docker exec -it some-mysql bash***

> ***-- root@75544a024f9b:/\# mysql -u root -p -h localhost***

> ***-- create database dbtest;***

<img src="img/media/image27.png" style="width:6.26042in;height:2.83333in" />

<span class="underline">3º Step:</span>

Delete the container(1º command), create a new container(2º command) and then Verify that the database is still created(3º, 4º and 5º command).

> ***-- docker container rm -f some-mysql***

> ***-- docker run --name some-mysql2 -v /opt/mysql:/var/lib/mysql -e MYSQL\_ROOT\_PASSWORD=asdasd -d mysql***

> ***-- docker exec -it some-mysql bash***

> ***-- root@75544a024f9b:/\# mysql -u root -p -h localhost***

> ***-- show databases;***

<img src="img/media/image28.png" style="width:6.40989in;height:3.26563in" />

<br>
</br>
</br>
</br>
</br>
</br>
</br>


<a name="1k"></a>


# **KUBERNETES**
</br>

# 1. Introduction
</br>

Nowadays, the most common scenario of an application deployment would be:

1.  A set of instances for running our app.

2.  An external load balancer for these instances.

3.  A set of databases that make persistent our app.

4.  Another load balancer that works internally between the instances and databases sets.
</br>
</br>

This deployment scenario imply a lot of configuration time and big costs. But, thanks to Kubernetes we can deploy it saving this costs.

Kubernetes its an open code system that allows the deployment, scalability, and application management in containers in an automated way.

This system can be broken down in the five following elements:

-   **Pod:** Minimum instance used in kubernetes. It will consist at least of one docker image, but can have more than one image even a database. This element is stateless and allows us to break down our full application in its differents process that will be running in differents pods that will interactuate between them.

-   **Deployment:** is the template that will instruct Kubernetes how to create the associated pods, how to boot the Docker container, how many replicas we want by default, etc.

-   **Service:** Pods are not visible neither accessible from outside themselves, for solving that is for what are the services, which act as load balancer and allows to access from outside and and inside (kubernetes node network).

-   **Volumes & Persistent volumes:** For apps which need storage.

-   **Ingress Controllers:** Redirects the traffic to the services.
</br>
</br>

<p align="center"><img src="img/media/image29.png" style="width:5.86458in;height:3.07292in" /></p>

<a name="2k"></a>
# 2. Installation and start.
</br>

We are going to work with minikube which is an environment to use Kubernetes in our laptop without having a production environment, either to use it as a developer, or to test it.

To download Minikube and install it, use the following commands:
</br>

> ***curl -Lo minikube [<span class="underline">https://storage.googleapis.com/minikube/releases/v0.30.0/minikube-linux-amd64</span>](https://storage.googleapis.com/minikube/releases/v0.30.0/minikube-linux-amd64)***
>
> ***&& chmod +x minikube***
>
> ***&& sudo cp minikube /usr/local/bin/***
>
> ***&& rm minikube***

</br>
<p align="center"><img src="img/media/image30.png" style="width:6.8092in;height:1.65104in"/></p>
</br>
</br>
</br>

Same for kubectl:
</br>

> ***curl -Lo kubectl [<span class="underline">https://storage.googleapis.com/kubernetes-release/release/v1.10.0/bin/linux/amd64/kubectl</span>](https://storage.googleapis.com/kubernetes-release/release/v1.10.0/bin/linux/amd64/kubectl)***
>
> ***&& chmod +x kubectl***
>
> ***&& sudo cp kubectl /usr/local/bin/***
>
> ***&& rm kubectl***
</br>
</br>

<p align="center"><img src="img/media/image31.png" style="width:6.25in;height:1.48944in" /></p>
</br>
</br>
</br>

Start the virtual machine with minikube (this step start the installation of the cluster).
</br>

> ***-- minikube start --vm-driver=virtualbox***

<p align="center"><img src="img/media/image32.png" style="width:6.30419in;height:1.81771in" /></p>

</br>
</br>
</br>

For checking the installation we can use this command:

***-- kubectl get nodes***

</br>
<p align="center"><img src="img/media/image33.png" style="width:5.90632in;height:0.84896in" /></p>

</br>
</br>
</br>

Last step, add the component ingress:
</br>
</br>
***-- minikube addons enable ingress***

</br>
<p align="center"><img src="img/media/image34.png" style="width:5.97396in;height:0.67926in" /></p>


</br>
</br>

# 3. Working with minikube

<a name="3k"></a>
## 3.1 Fault tolerance

Let's see how minikube automatically deploys pods when anyone of the running pods fails.
First, create a pod from a dockerhub image

> ***-- kubectl run pagweb --image alexisruiz00/aplicacionesweb:v1***


</br>
</br>

<p align="center"><img src="img/media/image35.png" style="width:5.9375in;height:0.39063in" /></p>

Once the pod is running, let’s delete it to see how minikube instantly deploys a new pod.

> ***-- kubectl get pods***

> ***-- kubectl delete pod/pagweb-59dc644f4d-cqlrn***

<p align="center"><img src="img/media/image36.png" style="width:5.90104in;height:2.74225in" /></p>

The resource Deployment can be also checked:

> ***-- kubectl get deploy***

<p align="center"><img src="img/media/image37.png" style="width:5.95313in;height:0.97686in" /></p>

## 3.2 Scalability

The amount of running pods can be increased whenever it is needed just using this command:

> ***-- kubectl scale deploy “deployName” --replicas=”amountWanted”***

For checking it:

> ***-- kubectl get pod -o wide***

<p align="center"><img src="img/media/image38.png" style="width:5.94271in;height:1.90397in" /></p>


</br>
</br>
</br>
</br>

## 3.3 Load Balancing

Minikube distributes the workload between all the pods.

To see it, first step, create a resource Service to access to the app:

> ***-- kubectl expose deployment “deploymentName” --port=80 --type=NodePortI***

<p align="center"><img src="img/media/image39.png" style="width:6.07375in;height:0.58854in" /></p>

Second, get the port of the application:

> ***-- kubectl get services***

<p align="center"><img src="img/media/image40.png" style="width:5.99479in;height:0.96345in" /></p>

Third, get the ip of the cluster where the app is running:

> ***-- minikube ip***

<p align="center"><img src="img/media/image41.png" style="width:5.97396in;height:1.73925in" /></p>

Finally, try to access to the web app, and see how internally the service redirect the connection to one of the running pods. The service will be redirecting the connection to the pod with less load.

> ***-- http://”ip”:”port”***

This case:

> ***-- http://192.168.99.100:80***

<p align="center"><img src="img/media/image42.png" style="width:5.875in;height:1.55208in" /></p>


</br>
</br>
</br>
</br>

## 3.4 Continuous updates

A quality of minikube, is the fact that we can make continious updates without shutting down the VM or making us run another one, with this simpy command:

> ***-- kubectl set image deployment pagweb pagweb=alexisruiz00/aplicacionesweb:v2***

<p align="center"><img src="img/media/image43.png" style="width:6.50145in;height:0.81771in" /></p>


</br>
</br>
</br>
</br>

## 3.5 Rollback

Minikube allows us to get previous version of the build. For this we can use this command:

> ***-- kubectl rollout undo deployment/pagweb***

<p align="center"><img src="img/media/image44.png" style="width:6.49479in;height:1.75535in" /></p>


</br>
</br>
</br>
</br>

## 3.6 Routing

It is possible to access to the app by a DNS name. We will use nip.io domain. It is necessary to create a file ingress.yaml.

It must contains the following information:

<p align="center">

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: pagweb
spec:
  rules:
  - host: pagweb.172.22.200.165.nip.io
    http:
      paths:
      - path: /
        backend:
          serviceName: pagweb
          servicePort: 80
</p>


<p align="center"><img src="img/media/image45.png" style="width:5.96875in;height:3.16667in" /></p>

Create the resource ingress:

> ***-- kubectl create -f ingress.yaml***

<p align="center"><img src="img/media/image46.png" style="width:5.97396in;height:0.84459in" /></p>

Check it:

> ***-- kubectl get ingress***

<p align="center"><img src="img/media/image47.png" style="width:5.96875in;height:0.80208in" /></p>

<p align="center"><img src="img/media/image48.png" style="width:5.98438in;height:1.60972in" /></p>
