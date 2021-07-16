# Introduction
By default, Ubuntu server LTS has DCHP enabled. This guide will have steps to set a static ip which is necessary to keep the kubectl synchronized with the IP addresses that where setup at the start. 

# ip -a 
- It is important to see what adapter you are using through ``ip -a``. This will vary from person to person. In my situation. I am connected via eth0. 
  - en3sop is also common. In the .yaml file, replace it with the adapter listed.
  - This is how you can see what IP address you are using

# Netplan configuration
- Go to the directory /etc/netplan.
  - There should be a file called ``50-cloud-init.yaml`` in this directory. 
  - Make a new file using called ``01-network-manager.yaml``. **Please note:** The file has to start with a set of numbers like "01" and end with **.yaml**
  - Use vim or nano to edit these files . It has to be in sudo privlege. 

# Modifying .yaml file
- Add the following lines below in ``01-network-manger.yaml`` and ``50-cloud-init.yaml`` in the ``/etc/netplan directory``.
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
     dhcp4: false
     addresses: [<ip address?]
     gateway4: <ip address>
     nameservers:
       addresses: [8.8.8.8,8.8.4.4]
```
# Apply configuration
- To try this configuration, use command ``sudo netplan try``
  - If it goes through smoothly, its going to ask if you would like to keep this configuration. 
  - If there are errors, it could be possible that you didn't set the address and gateway 4 address right. 

- To apply settings, use command ``sudo netplan apply``
  - Use ``ip -a`` to see if the IP has changed 
