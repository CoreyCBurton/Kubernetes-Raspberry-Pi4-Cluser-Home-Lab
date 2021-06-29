# Introduction
It is important to have a static ip address. This relates to the Kubeconfig file, it is set up for the specific IP addresses. 

# Netplan directory
- Go to the directory /etc/netplan
- You will see files here. Make sure you dont chose the one with the cloud 

- Add this to the YAML file
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

-sudo netplan try 
- sudo netplan apply 
