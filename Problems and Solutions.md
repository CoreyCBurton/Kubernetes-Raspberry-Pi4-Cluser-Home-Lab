# Introduction 
While setting up everything in this repo, I have ran into alot of issues but they have been solved. Below are some issues and their solution, I know everyone can make common mistakes. Here they are.

# Cgroup memory not enabled. 
After setting up your kubeconfig, it could be exciting... till this error shows After you run ``` kubectl get nodes -o wide ```.  

``` The connection to the server <ip> was refused - did you specify the right host or port? ```

Going back to your ``` /boot/firmware/cmdline.txt ``` and add the code below.

```
cgroup_memory=1
cgroup_enable=memory
swapaccount=1
```
# Kubectl command not found on MacOs.
I used MacOS as my local machine to lauch Linkerd. While have the Kubconfig file on my computer, Kubectl wasent recognized. Follow the code below to take advantage of ```Kubectl``` on your local machine.

```
rm '/usr/local/bin/kubectl'
brew link kubernetes-cli
brew install kubectl
```
Kubectl is now avaialbe on the mac termianl. 

# Linkerd Viz dashboard failed to open
When trying to open up Linkerd with the viz dashboard, I ran into this issue.
```
http://localhost:50750
Grafana dashboard available at:
http://localhost:50750/grafana
Opening Linkerd dashboard in the default browser
Failed to open Linkerd dashboard automatically
Visit http://localhost:50750 in your browser to view the dashboard
```
The problem with this is that it is a local host and if you launch it on one of your nodes, it wont open. You will have to open up Linkerd on a local machine with the kubeconfig file attached to it. 

# SSH key error.
When setting up your cluster server, you might run into this issue.
```
Error: unable to connect to 192.168.1.141:22 over ssh: ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain
```
To solve this, make sure you have ```ssh-copy-id ubuntu@<ip>``` and ```ssh-keygen``` every node before setting up. 

# DHCP enabled on Ubuntu Servers
- Ovetime, you will see that the IP adresses on your raspberry pis will change. This is because DHCP is enabled by default. View the static ip read me here.


