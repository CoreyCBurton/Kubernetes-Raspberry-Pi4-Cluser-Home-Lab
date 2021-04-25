# Introduction
Now that linkerd has been installed, running a demo app can test the networok. The guide I willow is on the [linkerd website](https://linkerd.io/2.10/getting-started/).

# Installing the demo app
This application runs a demo app using gRPC and HTTP calls to allow the user to vote on emojis. Enter the code below to start.
```
curl -sL https://run.linkerd.io/emojivoto.yml | kubectl apply -f -
```
Next is too port foward the demo app using
```
kubectl -n emojivoto port-forward svc/web-svc 8080:80
```
On your localhost:8080, you should see the web display of the emoji app. 
<img width="1440" alt="Screen Shot 2021-04-25 at 4 05 47 PM" src="https://user-images.githubusercontent.com/81980702/116009595-28c21f00-a5e0-11eb-9065-e320b979e32e.png">

# Adding Emojivote to Linkerd
using the command below, you can add Emojivote to Linkerd 
```
kubectl get -n emojivoto deploy -o yaml | linkerd inject | kubectl apply -f -
```
