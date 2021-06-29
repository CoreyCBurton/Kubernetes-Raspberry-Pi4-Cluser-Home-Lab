# Introduction
By default, Ubuntu server LTS has DCHP enabled. This guide will have steps to set a static ip which is necessary to keep the kubectl synchronized with the IP addresses setup at the start. 

# Netplan configuration
- Go to the directory /etc/netplan.
  - There should be some files listed. If there is a file such as ``50-cloud`` you can ignore this. 
  - Make a new file using called ``01-network-manager.yaml`` 
  - Please note the .yaml extenison and how it starts with 01
# ip -a 
It is important to see what adapter you are using through ip -a. This will vary from person to person. In my siutation, I am connected via eth0

# Modifying .yaml file
- Add this using the text edior vim or nano to set up the static ip address. '
   - This is an example, please modify it how you would like.
```
network:
  version: 2 
  renderer: networkd
  ethernets:
    eth0:
      addresses:
      - <ipaddress>
      gateway4: 192.168.1.1
      nameservers
         addresses:
         - 8.8.8.8
         - 8.8.4.4
```
# Apply netplan
-sudo netplan try 
- sudo netplan apply 
