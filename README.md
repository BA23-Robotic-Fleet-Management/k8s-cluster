# Experimental Kubernetes cluster

This repository contains example kubernetes manifests to deploy the ROS2 fleet manager
to kubernetes.

## Setup

### Setting up kubernetes with microk8s

```bash
apt install snapd
snap install microk8s --classic
microk8s start
microk8s status --wait
microk8s enable dns
microk8s config > ~/.kube/config
# This is only set to allow binding the zenoh daemon to port 7447 on the server.
# It is not required if you are planing to run the zenoh daemon in the standard
# kubernetes port range
echo "--service-node-port-range=7000-40000" >> /var/snap/microk8s/4595/args/kube-apiserver
```

### Installing k9s for convenience access to k8s:

```bash
mkdir k9s
cd k9s
wget https://github.com/derailed/k9s/releases/download/v0.27.4/k9s_Linux_amd64.tar.gz
tar xf k9s_Linux_amd64.tar.gz
sudo install k9s /usr/local/bin/k9s
```

## Deployment

Create ros namespace:

```
kubectl create namespace ros2
```

Apply all kubernetes manifests:

```
kubectl apply -f manifests/
```
