# Experimental Kubernetes Cluster

This repository contains sample Kubernetes manifests for deploying the ROS 2 [fleet management system](https://github.com/BA23-Robotic-Fleet-Management/fleet_management_system) to Kubernetes.

## Setup

### Setting up Kubernetes with Microk8s

```bash
sudo -i
apt install snapd
snap install microk8s --classic
microk8s start
microk8s status --wait
microk8s enable dns
microk8s config > ~/.kube/config
# This is only set to allow the Zenoh daemon to bind to port 7447 on the server.
# It is not required if you are planing to run the Zenoh daemon in the standard
# Kubernetes port range
echo "--service-node-port-range=7000-40000" >> /var/snap/microk8s/4595/args/kube-apiserver
```

### Installing k9s

This is only required for more convenient access and management to the cluster.

```bash
mkdir k9s
cd k9s
wget https://github.com/derailed/k9s/releases/download/v0.27.4/k9s_Linux_amd64.tar.gz
tar xf k9s_Linux_amd64.tar.gz
sudo install k9s /usr/local/bin/k9s
```

## Deployment

Creating the Kubernetes namespace:

```bash
sudo kubectl create namespace ros2
```

Applying all Kubernetes manifests:

```bash
sudo kubectl apply -f manifests/
```
