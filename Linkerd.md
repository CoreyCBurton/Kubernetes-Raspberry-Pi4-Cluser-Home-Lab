# Introduction
Linkerd seems to work like a charm with this setup. My experience with it has been great so far. I am going to follow this guide on the offical [Linkerd website](https://linkerd.io/2.10/getting-started/). If you have any other questions about your set up, they have an amazing guide so check it out. 

# Installing Linkerd CTL 
Just like installing K3Sup, we have to install the command-line interface. This allows you to interact with Linkerd through the terminal. Type in this command below.
```
curl -sL run.linkerd.io/install | sh
```
Afrer that runs through, you have to export the path which is in **/home/ubuntu/.linkerd2/bin**. The command below does this. 
``` 
export PATH=$PATH:/home/<user>/.linkerd2/bin
```
to veryify that the CTL is installed, we have to run a linkerd command. Use ```linkerd version``` and if it works, you should see this below.

```
Client version: stable-2.10.0
Server version: unavailable
```

# Validate the cluster
Before installing the Linkerd control plane, we have to valiadate that everything is in place. Run command ``` Linkerd check --pre ```. If everything checks out with green check marks, you are ready to move on. 

# Installing the Control Plane
Type this command in the console to install the control plane.

``` linkerd install | kubectl apply -f - ``` 

The next step is to make sure that everything installed properly by using command ``` linkerd check ```, if not then you will have to troubleshoot through the [Linkerd Website](https://linkerd.io/2.10/tasks/troubleshooting/) 
# Installing extensions 
To start off, the **viz** extenstion is going to be used for this homelab. It is also known as "Prometheus" which is the dashboard and metric component for the cluster. To install viz, enter the command below.

``` 
linkerd viz install | kubectl apply -f - # on-cluster metrics stack
```

# Optional extensions 
The linkerd setup guide also has other recommendations for Linkerd. One of them is Jaeger; a tracing system which can list proxies. The command below is too install it.
``` 
linkerd jaeger install | kubectl apply -f -
```
It also recommends multicluster components, to install that, use the command below.
```
linkerd multicluster install | kubectl apply -f - # multi-cluster components
```
Linkerd also points out that you can install buoyant, a thrid party dashboard. it isnt required but feel free to install it with the command below. 
```
curl -sL buoyant.cloud/install | sh
linkerd buoyant install | kubectl apply -f -
```
# Seeing what is active
Using command ``` Kubectl get ns ``` , you can see what is active. This homelab has has Buoyant, Multicluster, and Viz installed.
```
NAME                   STATUS   AGE
default                Active   2d13h
kube-system            Active   2d13h
kube-public            Active   2d13h
kube-node-lease        Active   2d13h
linkerd-multicluster   Active   2d5h
buoyant-cloud          Active   2d5h
linkerd                Active   25h
linkerd-viz            Active   24h
```
# Opening Linkerd with viz
After you choose what extensions to install, run ```linkerd check``` to make sure everything is validated. After that, run the command below and the dashboard will pull up. 
```
linkerd viz dashboard &
```
Now linkerd is installed onto your cluster.


 
