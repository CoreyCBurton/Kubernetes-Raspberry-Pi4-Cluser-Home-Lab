# Introduction
Now that you have the SD cards set up for Ubuntu 20.044.2 LTS and your Raspberry Pis on the platform, it is time to set up the server on each Raspberry Pi. 

#   Fix the resolution on the Pi (optional)
Once you boot up your Pi, the console seems very zoomed out. If that is the way you pefer it, that is completely fine. If you are like me and pefer a more zoomed in version, then follow these steps. Type this command in the console ```sudo dpkg-reconfigure console-setup ``` This will lead you to a user interface where it will ask what incoding to use. The option I picked was **UTF-8**. Then the screen will ask you what character to support, the one that I used is **Combined-Latin: Slavic Cyrlllic: Greek**. It will then ask you what font for the console, this is all up for user perference but the one I chose was the **TerminusBold**. Last but not least, it will ask you what font size you would like, the one that I chose was the **16x32(framebuffer only)**. Now that I have my console set up, it is time to move on to enabling cgroup memory.  

# Enabling cgroup memory 
In order for Kubernetes to work, we will have to modify the **cmdline.txt** by enabling cgroup memory. The directroy for **cmdline.txt** is **boot/firmware/cmdline.txt**. To know you are in the right place, you should see the line of code below. Leave it there, you are going to add to it.
```
net.ifnames=0 dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc
```
Using the **nano** editor while in root or sudo, please add this code to the .txt file. 
```
cgroup_memory=1
cgroup_enable=memory
swapaccount=1
```
# Getting the IP adress from the Raspberry Pi
If you know how to navigate around your router and you have the Raspberry Pi hooked up to your switch properly, then you can find the ip under Ubuntu in your router settings. If you want to find the ip using the terminal, follow these steps. Type in the console ``` ip a ```. Looking at what the console returned, find **eth0** and **inet** is listed with a set of numbers that ussaly starts with **192.xxx.x.xxx**; This is the ip address for the Pi you just set up. Next step is too add the SSH key.

# Setting the master node and SSH keys.
Once you have the IP address from all your Raspberry Pis, choose a main IP that will be the master node. The next step is too add the SSH keys to each Pi so when we set up the cluster, they can all connect and they are validated which sercures the network. On the master node, add each raspberry. First, you have to generate a SSH key with ``` ssh-keygen ```  and accept the prompts, the paraphrase is optional. After that, use ``` ssh-copy-id ubuntu@<ip> ``` on the three other Ips which will add the keys. The next step is to set up the cluster. 

# Renaming your Raspberry Pis. (optional)
In order to keep everything in order, I recommend naming your Raspberry Pis. I named my masternode "alpha" and contined labeling following "beta","charile",and "delta". In order to do this, you have to go into root by typing the command `sudo su`. After that type in this command below. 
```
sudo echo <NAME> > /etc/hostname
```
# IMPORTANT! 
do not set up the K3sup server on your node or Raspberry pi. It will lead to problems when trying to install Linkerd, the security mesh that goes along with K3sup. The kubeconfig file needs to be done on your local machine. You can connect to other machines using ``` ubuntu@<ip> ``` but this should only be done to set up when you arent using ``` kubectl```. Lets move on. 

# Setting up K3sup 
The guide that I am using is from [K3sup](https://github.com/alexellis/k3sup). The github page has alot of information and a very good README file to answer any questions. To start off make sure you are on the your local macine, **this is important**. The first step is too install K3up on the OS. You have to enter **sudo su** which puts you into root, which allows you to access everything that needs to be done. Once you are in root, enter:
```
curl -sLS https://get.k3sup.dev | sh # This line transfers the data from github which allows k3sup to be installed onto /usr/local/bin/
sudo install k3sup /usr/local/bin/ # This insalls k3sup from directory /usr/local/bin

k3ssup --help # If you have questions, use this command to pull up various commands. 
```
Once everything is done, you should see a red logo showing "K3sup" that list no errors. Just to make sure it is installed, you can always type in the terimnal ``` k3sup version ```

<img width="375" alt="Screen Shot 2021-04-11 at 2 13 52 AM" src="https://user-images.githubusercontent.com/81980702/114295615-efc86d00-9a6b-11eb-9060-f2738b4d05c5.png">
> What K3sup version returns in the terminal. 

# Setting up the cluster.
 The first step we have to do init the master node with K3sup. The command below shows what you have to do. 
 ```
 k3sup install --ip <MASTER_NODE> --user ubuntu
 ```
 Lets break it down.
 ``` 
 k3sup install # Bootstraps Kubernetes with k3u
 --ip # sets the ip for the master node
 --user # States the user, Ubuntu was used for me but root is also common.
 ``` 
 Now that we have initated the master node, it is time to add the other Raspberry Pis to the cluster. The command below initates it.
 
 ```  
 k3sup join --ip <NODE_IP> --server-ip <MASTER_NODE> --user ubuntu
 ``` 
 lets break it down
 ``` 
 k3sup join # This initates the join command to enter the master node 
 --ip # The ip that connect to the master node 
 --server-ip # The master node ip that inits the cluster
 --user # states the user
 ``` 
 Once you add each Raspberry Pi to the server than it is setup! To make it more effiecnt there is a way to automate it through a script.
 
 # Script to init the cluster server
 Avery Wagar, the OP that posted on r/homelabs whose [blog](https://averywagar.com/post/k3s-pi/) inspired me to do this bulid wrote a scipt to automate this process. Below is the script he has created called **init_pis.sh**.
 
 ``` 
 #!/bin/bash

MASTER_NODE=$1
NODE1=$2
NODE2=$3
NODE3=$4

# Init MASTER_NODE
echo "Initializing $MASTER_NODE as master node."
k3sup install --ip $MASTER_NODE --user ubuntu

# Join nodes
for NODE_IP in $NODE1 $NODE2 $NODE3
do
  echo "Joining $NODE_IP to the cluster..."
  k3sup join --ip $NODE_IP --server-ip $MASTER_NODE --user ubuntu
done
```
to init, use this command below 
```
./init_pis.sh <master-ip> <node-ip> <node-ip> <node-ip>
```
You can do it manually but thanks to Avery and his talent, he has automated the process. 

# Exporting the KUBECONFIG and showing the nodes in your cluster.
Now that we initiated the cluster server, it is time to export the config so we can list the nodes. Input the command below to export. Keep in mind, your directory might be different that mine.
```
export KUBECONFIG=/home/ubuntu/kubeconfig
```
Now that the config is exported, use this command to show the nodes.
```
kubectl get nodes -o wide
```
The list of nodes should look like this.
```
NAME      STATUS   ROLES    AGE     VERSION        INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAINER-RUNTIME
beta      Ready    <none>   2m24s   v1.19.9+k3s1   192.168.1.144   <none>        Ubuntu 20.04.2 LTS   5.4.0-1028-raspi   containerd://1.4.4-k3s1
alpha     Ready    master   27m     v1.19.9+k3s1   192.168.1.99    <none>        Ubuntu 20.04.2 LTS   5.4.0-1033-raspi   containerd://1.4.4-k3s1
charlie   Ready    <none>   76s     v1.19.9+k3s1   192.168.1.20    <none>        Ubuntu 20.04.2 LTS   5.4.0-1028-raspi   containerd://1.4.4-k3s1
delta     Ready    <none>   22s     v1.19.9+k3s1   192.168.1.41    <none>        Ubuntu 20.04.2 LTS   5.4.0-1028-raspi   containerd://1.4.4-k3s1
``` 
# Troubleshoot
If you get an error stating 
```
The connection to the server 192.168.1.75:6443 was refused - did you specify the right host or port?
```
You have to make sure you that /boot/firmware/cmdline has the correct information. 
