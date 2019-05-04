 **Project: “Cloud Computing in European schools”**  
<img src="/img/cloud-computing-logoproject.jpg" height="100" width="170"/>

 Number: Project: 2017-1-ES01-KA202-038471

<img src="/img/cofinanciadoEN.png" height="50" width="200"/> <img src="/img/logoIES-Modificado.png" height="75" width="200"/>  




# Introduction to PaaS: develop, deploy, run and manage apps on the Cloud  



#### Disclaimer
&nbsp;&nbsp;&nbsp;  *"The European Commission support for the production of this publication does not constitute an endorsement of the contents which reflects the views only of the authors, and the Commission cannot be held responsible for any use which may be made of the information contained therein."*




#### Author

&nbsp;&nbsp;&nbsp;  This material has been produced by José Luis Rodríguez Rodríguez under the Creative Commons licence:  <img src="/img/Licencia-Tipo2.png" height="25" width="75"/>  




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

Docker version:

HACER CAPTURA CON DOCKER VERSION






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

-   

Dockerfile must be created in the vagrant fold of /home

<p align="center"><img src="img/media/image11.png" style="width:6.29167in;height:1.66667in" /></p>

<span class="underline">3ºStep:</span>

Create the docker image. using the following command:

***-- docker build -t accountName/aplicacionesweb:v1***

<p align="center"><img src="img/media/image12.png" style="width:6.461in;height:0.93229in" /></p>

And use this command to see which images you have:

> ***-- docker image ls***

<p align="center"><img src="img/media/image13.png" style="width:6.34394in;height:0.88021in" /></p>

<span class="underline">4ºStep</span>

Upload our docker image to a repository in Dockerhub ([<span class="underline">hub.docker.com</span>](https://hub.docker.com/))

Log in our dockerhub account:

***-- docker login***

<p align="center"><img src="img/media/image14.png" style="width:6.07292in;height:1.0625in" /></p>

Upload the docker image to a repository in our account:

***-- docker push accountName/repositoryName:”imageName”***

<p align="center"><img src="img/media/image15.png" style="width:6.44329in;height:0.69271in" /></p>

<span class="underline">5ºStep</span>

<span class="underline"> </span>

<span class="underline"> </span> Download a docker image from dockerhub:

***-- docker pull accountName/repositoryName:”imageName”***

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

***-- docker build -t accountName/aplicacionweb:v2***

<p align="center"><img src="img/media/image21.png" style="width:6.55035in;height:1.78646in" /></p>

<span class="underline">8.2º Step</span>

Upload the new image.

***-- docker push accountName/aplicacionesweb:v2***

<p align="center"><img src="img/media/image22.png" style="width:6.30922in;height:0.53646in" /></p>

<span class="underline">8.3º Step</span>

Download the new image to the production environment.

***-- docker pull accountName/aplicacionesweb:v2***

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

***docker run --name some-mysql -v /opt/mysql:/var/lib/mysql -e MYSQL\_ROOT\_PASSWORD=asdasd -d mysql***

<img src="img/media/image26.png" style="width:6.0625in;height:1.5625in" />

<span class="underline">2º Step:</span>

Create a database called dbtest.

***docker exec -it some-mysql bash***

***root@75544a024f9b:/\# mysql -u root -p -h localhost***

***create database dbtest;***

<img src="img/media/image27.png" style="width:6.26042in;height:2.83333in" />

<span class="underline">3º Step:</span>

Delete the container(1º command), create a new container(2º command) and then Verify that the database is still created(3º, 4º and 5º command).

***docker container rm -f some-mysql***

***docker run --name some-mysql2 -v /opt/mysql:/var/lib/mysql -e MYSQL\_ROOT\_PASSWORD=asdasd -d mysql***

***docker exec -it some-mysql bash***

***root@75544a024f9b:/\# mysql -u root -p -h localhost***

***show databases;***

<img src="img/media/image28.png" style="width:6.40989in;height:3.26563in" />
