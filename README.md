# Introduction
This repo shows the process of how to create a Kubernetes (k3s) cluster out of Raspberry Pis. Through the hardware setup and creating the Kubectl config, the cluster can be utilized. 

# The reason behind this project
Having a home lab is important and there are many ways to set one up for what's needed to be done. Kubernetes is a powerful container orchestration utility and it's a skill I would like to have. Approaching this, there are multiple ways to create a cluster so that Kubernetes can operate. There's always the cloud that will utilize AWS or Azure which is great, but I wanted hands-on equipment. Raspberry Pis were great for this. After setting up Kubectl and realizing that I achieved the cluster, it was a matter of learning more about what I can do with it. I learned a lot and most importantly, I have a home lab that can host future projects.

# What I have learned 
- How to install Ubuntu 20.04 LTS on Raspberry Pis 
- How to navigate around Linux and how it functions 
- Various commands utilizing Kubectl 
- How to add and manage containers using Kubernetes 

# Index
- Intial set up 
  - [Hardware setup](https://github.com/CoreyCBurton/Kubernetes-Raspberry-Pi4-Cluser-Home-Lab/blob/main/Hardware%20Setup.md)
  - [Software setup (Installing K3s)](https://github.com/CoreyCBurton/Kubernetes-Raspberry-Pi4-Cluser-Home-Lab/blob/main/Software%20Setup.md)
  - [Static IP setup using netplan](https://github.com/CoreyCBurton/Kubernetes-Raspberry-Pi4-Cluser-Home-Lab/blob/main/StaticIPaddress.md)
  - [Problems and Solutions](https://github.com/CoreyCBurton/Kubernetes-Raspberry-Pi4-Cluser-Home-Lab/blob/main/Problems%20and%20Solutions.md) 
  
- Services added to cluster 
  - [Linkerd Mesh](https://github.com/CoreyCBurton/Kubernetes-Raspberry-Pi4-Cluser-Home-Lab/blob/main/Linkerd.md)
  - [Grafana](https://github.com/CoreyCBurton/Kubernetes-Raspberry-Pi4-Cluser-Home-Lab/blob/main/Grafana.md)






