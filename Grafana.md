# Introduction
Having Prometheus and Grafana on your Raspberry Pi is super important. Using Helm charts that are provided with Kubernetes, we can achieve this.

# Cluster-monitoring
Following this (repo)[https://github.com/carlosedp/cluster-monitoring], We can have an optimized Grafana-dashboard for our raspberry pi cluster. The first step is to clone the repo using the command below
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
suffixDomain: `192.168.1.132.nip.io` ```
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
