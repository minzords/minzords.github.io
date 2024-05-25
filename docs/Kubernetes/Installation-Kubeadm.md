---
title: Installer un cluster Kubernetes
description: 
published: true
date: 2023-10-19T10:06:42.807Z
tags: 
editor: markdown
dateCreated: 2023-10-19T10:01:41.586Z
---

# Installation de Kubernetes
```bash
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
```
  sudo apt-get update
  sudo apt-get install -y kubelet kubeadm kubectl
  sudo apt-mark hold kubelet kubeadm kubectl
```
```
  sudo tee /etc/modules-load.d/k8s.conf <<EOF
  overlay
  br_netfilter
  EOF
```

```
  sudo modprobe overlay
  sudo modprobe br_netfilter
```

```
  sudo tee /etc/sysctl.d/kubernetes.conf<<EOF
  net.bridge.bridge-nf-call-ip6tables = 1
  net.bridge.bridge-nf-call-iptables = 1
  net.ipv4.ip_forward = 1
  EOF
```

```
sudo sysctl --system
```

# Installation de Containerd
```
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  sudo chmod a+r /etc/apt/keyrings/docker.gpg
  echo \
    "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
  sudo apt install -y containerd.io
```

```
  sudo mkdir -p /etc/containerd
  containerd config default | sudo tee /etc/containerd/config.toml
  sudo systemctl restart containerd
  sudo systemctl enable containerd
```

# Ininitialisation du Control Plane
```bash
  kubeadm init \
    --pod-network-cidr=192.168.89.0/16
```
192.168.89.0 sera le réseau local des conteneurs.

# Gestion du reseau avec flannel
```bash
  wget https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
  vi kube-flannel.yml
```
Et modifier le champ Network pour indiquer le réseau local dans notre exemple: 192.168.89.0/16

```bash
  kubectl apply -f kube-flannel.yml
```

# Mettre en place l'autocompletion
```
	apt install bash-completion
	echo "source <(kubectl completion bash)" >> ~/.bashrc
	source ~/.bashrc
```


# Integrer un noeud au cluster
```bash
  kubeadm join 10.0.2.100:6443 --token hpr49r.v40bgx8z06gk4itf --discovery-token-ca-cert-hash sha256:f95f3c004c9757265e395b68654c66ce9cbba22eb2129ebde2f2b0c29107f41a
```
Les paramètres pour rejoindre le Control Plane a été donné au moment de l'initialisation du Control Plane.


Sources: [computingforgeeks](https://computingforgeeks.com/install-kubernetes-cluster-on-debian-12-bookworm)