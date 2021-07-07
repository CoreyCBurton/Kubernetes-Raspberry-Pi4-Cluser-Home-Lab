# Introduction
Now that you have the SD cards set up for Ubuntu 20.044.2 LTS and your Raspberry Pis on the platform, it is time to set up the server on each Raspberry Pi. 

# Enabling cgroup memory 
In order for Kubernetes to work, we will have to modify the **cmdline.txt** by enabling cgroup memory. The directroy for **cmdline.txt** is **boot/firmware/cmdline.txt**. To know you are in the right place, you should see the line of code below. Leave it there, you are going to add to it.
```
net.ifnames=0 dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=LABEL=writable rootfstype=ext4 elevator=deadline rootwait fixrtc
```
Using the **nano** or **Vim** editor while in root or sudo, please add this code to the .txt file. 
```
cgroup_memory=1
cgroup_enable=memory
swapaccount=1
```
# Getting the IP adress from the Raspberry Pi
- If you know how to navigate around your router and you have the Raspberry Pi hooked up to your switch properly, then you can find the ip under Ubuntu in your router settings. If you want to find the ip using the terminal, follow these steps. Type in the console ``` ip a ```. Looking at what the console returned, find **eth0** and **inet** is listed with a set of numbers that ussaly starts with **192.xxx.x.xxx**; This is the ip address for the Pi you just set up. Next step is too add the SSH key.
  - If you have a linux distribution such as Kali Linux, you can also use the command ``netdiscover``to find the addresses to each PI.

# Setting the master node and SSH keys.
Once you have the IP address from all your Raspberry Pis, choose a main IP that will be the master node. The next step is too add the SSH keys to each Pi so when we set up the cluster, they can all connect and they are validated which sercures the network. On the master node, add each raspberry. First, you have to generate a SSH key with ``` ssh-keygen ```  and accept the prompts, the paraphrase is optional. After that, use ``` ssh-copy-id ubuntu@<ip> ``` on the three other Ips which will add the keys. The next step is to set up the cluster. 

# Renaming your Raspberry Pis. (optional)
In order to keep everything in order, I recommend naming your Raspberry Pis. I named my masternode "Alpha" and continued labeling following "Beta,"Charile",and "Delta". **Alpha holds the kubeconfig while I also have one on my local macbook**. In order to do this, you have to go into root by typing the command `sudo su`. type the command below to change the name. 
```
sudo echo <NAME> > /etc/hostname
```
# IMPORTANT! 
Keep track of where you are installing the **kubeconfig** which is where you run the script below. As listed [here](https://github.com/alexellis/k3sup#getting-access-to-your-kubeconfig) in the orginal K3sup, it shows there can be a problem later on with ssh validation if you try to use kubectl on your nodes. **Always use kubectl on a local machine that has the kubeconfig file handy**.

# Setting up K3sup 
The guide that I am using is from [K3sup](https://github.com/alexellis/k3sup). The repo page has alot of information and a very good README file to answer any questions. To start off, make sure you are on the machine that you would like to store the kubeconfig file. **this is important**. The first step is too install K3up on the OS. You have to enter **sudo su** which puts you into root, which allows you to access everything that needs to be done. Once you are in root, enter
```
curl -sLS https://get.k3sup.dev | sh # This line transfers the data from github which allows k3sup to be installed onto /usr/local/bin/
sudo install k3sup /usr/local/bin/ # This insalls k3sup from directory /usr/local/bin

k3sup --help # If you have questions, use this command to pull up various commands. 
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
 k3sup install # Bootstraps Kubernetes with k3s
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
 Once you add each Raspberry Pi to the server than it is setup! To make it more effiecnt, there is a way to automate it through a script.
 
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
Now that we initiated the cluster server, it is time to export the config so we can list the nodes. Input the command below to export. 
```
export KUBECONFIG='pwd'/kubeconfig
```
Now that the config is exported, use this command to show the nodes.
```
kubectl get nodes -o wide
```
The list of nodes should look like this.
```
NAME      STATUS     ROLES    AGE    VERSION        INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAINER-RUNTIME
alpha     Ready      <master> 117m   v1.19.9+k3s1   192.168.1.76    <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   containerd://1.4.4-k3s1
delta     Ready      <none>   120m   v1.19.9+k3s1   192.168.1.17    <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   containerd://1.4.4-k3s1
chairle   Ready      <none>   121m   v1.19.9+k3s1   192.168.1.252   <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   containerd://1.4.4-k3s1
beta      Ready      <none>   126m   v1.19.9+k3s1   192.168.1.121   <none>        Ubuntu 20.04.2 LTS   5.4.0-1034-raspi   containerd://1.4.4-k3s1
``` 

