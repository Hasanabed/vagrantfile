# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"


  #STARTUP SERVER CONFIG
 # Create a private network, which allows host-only access to the machine
  # using a specific IP.
   config.vm.network "private_network", ip: "192.168.56.10"
 # Create a bridge, which allows direct access to the machine from wifi
   config.vm.network "public_network", bridge: "Intel(R) Dual Band Wireless-AC 8265", auto_config: true
  # Create a bridge, which allows direct access to the machine from the ethernet
   config.vm.network "public_network", bridge: "Intel(R) Ethernet Connection (4) I219-LM", auto_config: true

 # set up Docker in the new VM:
  config.vm.provision :docker
 # install docker-compose into the VM and run the docker-compose.yml file - if it exists -  whenever the  VM starts 
  config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", run:"always"

  config.vm.provider "virtualbox" do |vb|
 #   # Display the VirtualBox GUI when booting the machine
 #  vb.gui = true
 #
 #   # Customize the amount of memory on the VM:
 # CONFIG FOR ROCKET SERVER
   vb.customize ["modifyvm", :id, "--memory", "16384", "--cpus", "4"]
 #CONFIG TO RUN ON LAPTOP
 #  vb.memory = "4096"
 
  end
 # Enable SSH password authentication
 config.vm.provision "shell", inline: <<-SHELL
   sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/g' /etc/ssh/sshd_config
   sed -i 's/#PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
   service ssh restart
   SHELL

# Install packages and virtualbox additions
#firefox: Graphical web browser
#w3m: text based web browser, example: w3m -v http://www.google.com
# xfce4: Graphical environment
#apache2: web server
#ipmitool: tool for ipmi commands
#vlan: tool for 801.q config
#aptly: tool for repository creation.
#vsftpd
#vnc4server VNC SERVER
 config.vm.provision "shell", inline: "sudo apt-add-repository ppa:ansible/ansible"
 config.vm.provision "shell", inline: "sudo apt-get update"
 config.vm.provision "shell", inline: "sudo apt-get install -y ansible apache2 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11 ipmitool vlan vsftpd aptly w3m"

#Add 801.q to /etc/modules 
#Add 801.q adapters to ether interface:
#REMEMBER TO REPLACE WITH LOCAL IP ADDRESSES

#VLAN 101 Interface IP:
#VLAN 101 netmask:
#VLAN 101 Default Gateway IP:

#VLAN 4091 Interface IP:
#VLAN 4091 netmask:
#VLAN 4091 Default Gateway IP:

#VLAN 4089 Interface IP:
#VLAN 4089 netmask:
#VLAN 4089 Default Gateway IP:

#VLAN 201 Interface IP:
#VLAN 201 netmask:
#VLAN 201 Default Gateway IP:

 #config.vm.provision "shell", inline: <<-SHELL
 #  sudo echo '8021q' >> /etc/modules
 #  echo 'auto enp0s10.101' >> /etc/network/interfaces
 #  echo 'iface enp0s10.101 inet static' >> /etc/network/interfaces
 #  echo 'address 146.250.113.62' >> /etc/network/interfaces
 #  echo 'netmask 255.255.255.192' >> /etc/network/interfaces
 #  echo 'vlan-raw-device enp0s10' >> /etc/network/interfaces
 #  echo 'auto enp0s10.4091' >> /etc/network/interfaces
 #  echo 'iface enp0s10.4091 inet static' >> /etc/network/interfaces
 #  echo 'address 146.250.113.110' >> /etc/network/interfaces
 #  echo 'netmask 255.255.255.240' >> /etc/network/interfaces
 #  echo 'vlan-raw-device enp0s10' >> /etc/network/interfaces
 #  echo 'auto enp0s10.4089' >> /etc/network/interfaces
 #  echo 'iface enp0s10.4089 inet static' >> /etc/network/interfaces
 #  echo 'address 146.250.113.118' >> /etc/network/interfaces
 #  echo 'netmask 255.255.255.248' >> /etc/network/interfaces
 #  echo 'vlan-raw-device enp0s10' >> /etc/network/interfaces
 #  echo 'auto enp0s10.201' >> /etc/network/interfaces
 #  echo 'iface enp0s10.201 inet static' >> /etc/network/interfaces
 #  echo 'address 146.250.113.158' >> /etc/network/interfaces
 #  echo 'netmask 255.255.255.240' >> /etc/network/interfaces
 #  echo 'vlan-raw-device enp0s10' >> /etc/network/interfaces
 #  SHELL
 # Permit anyone to start the GUI
 #config.vm.provision "shell", inline: "sudo sed -i 's/allowed_users=.*$/allowed_users=anybody/' /etc/X11/Xwrapper.config"
 
 
 # trigger reload
 config.vm.provision :reload

#install rocket server file
 
#show VM IP address
   echo '*********************************************'  
   echo 'VNC SERVER AVAILABLE (Display :1 :2 :3) Password: vncpassword'
   echo '*********************************************'
   echo 'Portainer URL : IPADDRESS:9000'
   echo '*********************************************'
   echo 'IP ADDRESS FOR START UP SERVER:'

   ip a | grep enp0s9

   echo '*********************************************'
   echo 'SSH : USER: vagrant PASSWORD: vagrant'

   SHELL



end
