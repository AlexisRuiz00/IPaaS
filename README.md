 **Project: “Cloud Computing in European schools”**  
<img src="/img/cloud-computing-logoproject.jpg" height="100" width="170">

 Number: Project: 2017-1-ES01-KA202-038471

<img src="/img/cofinanciadoEN.png" height="50" width="200"> <img src="/img/logoIES-Modificado.png" height="75" width="200">  

### **<span class="underline">Docker</span>**

### **<span class="underline">1- Docker installation: virtual machine managed by Vagrant.</span>**

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

***vagrant box add ubuntu/bionic64 --provider virtualbox***
<p align="center"><img src="img/media/image6.png" style="width:4.98958in;height:2.07292in" /></p>

*(This is the box (image) that it is going to be use as basis to install docker)*

<span class="underline">5º Step:</span>

Checking that everything has worked correctly:

> ***-- vagrant box list***

<p align="center"><img src="img/media/image7.png" style="width:6.27083in;height:1.51389in" /></p>

<span class="underline">6º Step:</span>

With the following command, the ubuntu box downloaded will be started applying the Vagrantfile configuration

> ***-- vagrant up***

<p align="center"><img src="img/media/image8.png" style="width:5.85876in;height:0.83854in" /></p>

<span class="underline">7º Step</span>

Finally, we can access to the created box by ssh connection and check if docker is been successfully installed.

SSH connection:

> ***-- vagrant ssh***

<p align="center"><img src="img/media/image9.png" height="300" width="600"/></p>
