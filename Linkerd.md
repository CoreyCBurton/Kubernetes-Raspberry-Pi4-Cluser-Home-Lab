curl -sL run.linkerd.io/install | sh
export PATH=$PATH:/home/ubuntu/.linkerd2/bin
linkerd version
> Client version: stable-2.10.0
> Server version: unavailable

linkerd check --pre
<img width="459" alt="Screen Shot 2021-04-11 at 4 47 46 PM" src="https://user-images.githubusercontent.com/81980702/114322424-cc420880-9ae5-11eb-8fbe-3efa0f41b1e4.png">

linkerd install | kubectl apply -f -

linkerd viz install | kubectl apply -f -

linkerd jaeger install | kubectl apply -f -

linkerd multicluster install | kubectl apply -f -

curl -sL buoyant.cloud/install | sh
 export PATH=$PATH:/home/ubuntu/.linkerd2/bin
 
 
