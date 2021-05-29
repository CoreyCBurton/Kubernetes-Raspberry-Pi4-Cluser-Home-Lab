# Introduction
Having Prometheus and Grafana on your Raspberry Pi is super important. Using Helm charts that are provided with Kubernetes, we can achieve this.

# Cluster-monitoring
Following this [repo](https://github.com/carlosedp/cluster-monitoring), We can have an optimized Grafana-dashboard for our raspberry pi cluster. The first step is to clone the repo using the command below
```
git clone https://github.com/carlosedp/cluster-monitoring.git
```
Cd into the directory CLuster monitoring 

# Editing vars.jsonnet
Using command ``sudo nano vars.jsonnet`` we can edit the config to match our Raspberry Pi settings.

Under the k3s config, you want to add your master ip. It should look like this below 
```
k3s:{
  enabled: true,
  master_ip: [<MasterNode>]
}
```
Below that, The domain suffix needs to be editied to one of your worker nodes.
```
suffixDomain: `192.168.1.132.nip.io` 
```

# Installing make on MacOS
* Using the command `` brew install make`` we can download the make tool which will allow us to finish installing Grafana. 

# Installing Golang on MacOS
Following this [guide](https://golang.org/doc/install). Download the package file and verify using the command below.
```
$ go version
```
# Installing command line tools 
```
xcode-select --install
```

# Installing Grafana
```
$ make vendor
$ make
$ make deploy

# Or manually:

$ make vendor
$ make
$ kubectl apply -f manifests/setup/
$ kubectl apply -f manifests/
```
# The process of installing Grafana using make
Using the command `` kubectl apply -f manifests/setup/ ``, it creates a namespace called monitoring which is deploying Grafana to the pods 

Using the command ``kubectl get pods -n monitoring `` you can see the output below that everything is deployed
```

NAME                                  READY   STATUS    RESTARTS   AGE
prometheus-operator-67755f959-7rv92   2/2     Running   0          4m7s
arm-exporter-p5kwx                    2/2     Running   0          3m52s
node-exporter-ptf5q                   2/2     Running   0          3m48s
prometheus-adapter-585b57857b-rmmh5   1/1     Running   0          3m48s
node-exporter-7svh9                   2/2     Running   0          3m48s
arm-exporter-6qwlx                    2/2     Running   0          3m52s
alertmanager-main-0                   2/2     Running   0          3m52s
node-exporter-2bd24                   2/2     Running   0          3m48s
arm-exporter-527k7                    2/2     Running   0          3m52s
arm-exporter-f2h9z                    2/2     Running   0          3m52s
kube-state-metrics-6cb6df5d4-pnvsl    3/3     Running   0          3m49s
node-exporter-hhl8v                   2/2     Running   0          3m48s
prometheus-k8s-0                      3/3     Running   1          3m46s
grafana-784d46dcb-rgmwf               1/1     Running   0          3m49s


```

# Open Grafana 
using the command below allows you to see the host name 
```
kubectl get ingress -n monitoring
```
Ho the the address and it allows you to see what is there. 











