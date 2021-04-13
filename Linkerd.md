# Indroduction
Linkerd seems to work like a charm with this setup. My experience with it has been great so far. I am going to follow this guide on the offical [linkerd website](https://linkerd.io/2.10/getting-started/). If you have any other questions about your set up, they have an amazing guide so check it out. 

# Installing Linkerd CTL 
Just like installing K3Sup, we have to install the command-line interface. This allows you to interact with Linkerd through the terminal. Type in this command below.
```
curl -sL run.linkerd.io/install | sh
```
Afrer that runs through, you have to export the path which is in **/home/ubuntu/.linkerd2/bin**. The command below does this. 
``` 
export PATH=$PATH:/home/ubuntu/.linkerd2/bin
```
to veryify that the CTL is installed, it is time to run a linkerd command through. Use ```linkerd version``` and if it works, you should see this below.

```
> Client version: stable-2.10.0
> Server version: unavailable
```
# Validate the cluster
Before installing the Linkerd control plane, we have to valiadate that everything is in place. Run command ``` Linkerd check --pre ````.  





linkerd check --pre
<img width="459" alt="Screen Shot 2021-04-11 at 4 47 46 PM" src="https://user-images.githubusercontent.com/81980702/114322424-cc420880-9ae5-11eb-8fbe-3efa0f41b1e4.png">

linkerd install | kubectl apply -f -

linkerd viz install | kubectl apply -f -

linkerd jaeger install | kubectl apply -f -

linkerd multicluster install | kubectl apply -f -

curl -sL buoyant.cloud/install | sh
 export PATH=$PATH:/home/ubuntu/.linkerd2/bin
 
 export KUBECONFIG=/home/ubuntu/kubeconfig  
 
