# vagrantfile
vagrantfile and docker compose file to launch basic environment

DEPLOY STARTUP SERVER
=====================

### The following documents describes the process to spin up a VM to be used as jump server and installation toolkit for DC deployments. Some customization of the vagrant file is needed, mainly IP addresing for connectivity towards SDI/HDS


### CURRENT FEATURES:

	- Ubuntu Server 16.04
	- VNC server ( 3 separate sessions available)
	- Rocket Server containerized basic install
	- 801.Q config for interface towards DC ( IP address of local DCGW needs to be updated manually on the Vagrantfile)
	- Docker Compose file to orchestrate the provisioning of more services.
	- Customize the RAM/CPU count as needed (Currently set to 16Gb RAM, 4 cores )
	- The local folder C:\TEST\ on your machine is synched to the VM folder \Vagrant\
			o We can move files into the machine this way with no issues
	
### In progress:
	- Containerize LDAP server for SDI deployment ( We have the .sh scripts to quickly set it up, I just need some help creating a container image. 	
	- Enable Docker registry for private container images ( Rocket Server, LDAP, etc). This would avoid keeping container images locally, and let docker-compose download them on start up).



### INSTRUCTIONS:
 
## 1-) Install the following software in windows:
	- VAGRANT
			o https://www.vagrantup.com/downloads.html
	- VIRTUAL BOX
			o https://www.virtualbox.org/wiki/Downloads
			 
## 2-) Create a directory on you C: drive, example : C:\TEST\
## 3-) Execute the following commands (same commands for either Win or Linux OS):
               C:\TEST>vagrant plugin install vagrant-reload
               C:\TEST>vagrant plugin install vagrant-docker-compose




## 4-) If your already have a VM deployed:
		a. Destroy the previous VM:
			 C:\TEST>vagrant destroy -f
        If this is a new install execute the following command:
	        C:\TEST>vagrant init ubuntu/xenial64

## 5-) Delete the file named “Vagrantfile” that will now appear on the directory.
		
	
## 6-) Copy this files to  Vagrantfile to  C:\TEST or use git clone
	Vagrantfile
	Docker-compose.yml
	rs_cu_v311.tar
	** The last file is the rocket server container image.
	*** EDIT the Vagrantfile with the correct IP addresses for the site.
	
## 7-) Execute the following command:
               C:\TEST>vagrant up
 
A clean VM machine with Ubuntu Server 16.04 will be downloaded from the Canonical cloud image repository and configured with some packages.
 
### ACCESS INSTRUCTIONS:

- The values for the IP address currently assigned to the external IP will be displayed at the end of the Vagrant Script execution. Follow the instructions below.
- Use the command:
-       vagrant ssh
-   This will provide direct access to the VM from the HOST machine.
-   
# VNC instructions:
		○ There is a containerized service running:
			o Vnc server
			o Firefox
			o Chromium
		○ Connect using your VNC client:
			o Hostname : X where 
				□ X is the session (1, 2 or 3)
				□ Hostname: IP address of the target startup server, in this case, your PC.
# Rocket Server instructions:
		○ Open a web brower to IPADDRESS:32771
# Portainer:
		○ Open a web brower to IPADDRESS:9000


### TROUBLESHOOTING TIPS:

## Inaccesible VM:

	Get the uuid:
		VBoxManage list vms
	Remove the machine:
		VBoxManage unregistervm <uuid>

## CRASHES because of no screen available:

	- Install XMING locally
	- Change the local vagrant file so no GUI is opened.

## ADD A DEFAULT ROUTE

	sudo route add default gw 192.168.8.1 enp0s9

	sudo route delete default gw 10.0.2.2 enp0s3

## VNC server:

	netstat -tulpn
	sudo  ufw status verbose

