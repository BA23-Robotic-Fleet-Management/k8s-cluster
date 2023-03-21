# Experimental Kubernetes cluster

## Setup

minikube (Not prefered):

```bash
mkdir minikube
cd minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
# Run the next command as a normal user and not root
minikube start --extra-config=apiserver.service-node-port-range=1-65535
# Alias for kubectl
echo 'alias kubectl="minikube kubectl --"' >> ~/.bashrc
```

microk8s (prefered):

```
sudo apt install snapd
sudo snap install microk8s --classic
sudo usermod -a -G microk8s ubuntu
newgrp microk8s
microk8s start
microk8s status --wait
microk8s enable dns
microk8s config > ~/.kube/config
sudo echo "--service-node-port-range=7000-40000" >> /var/snap/microk8s/4595/args/kube-apiserver
```

k9s:

```bash
mkdir k9s
cd k9s
wget https://github.com/derailed/k9s/releases/download/v0.27.3/k9s_Linux_amd64.tar.gz
tar xf k9s_Linux_amd64.tar.gz
sudo install k9s /usr/local/bin/k9s
```

## Deployment

Create ros namespace:

```
kubectl create namespace ros2
```

Deploy zenoh:

```
kubectl apply -f zenoh.yaml
```

Deploy fleet-manager:

```
kubectl apply -f fleet-manager.yaml
```
