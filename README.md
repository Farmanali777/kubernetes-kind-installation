# kubernetes-kind-installation
Kubernetes (KIND) local cluster setup with Docker and kubectl for development and testing.

🚀 KIND + Docker + kubectl Installation Guide (Ubuntu)

This guide explains how to install Docker, KIND, and kubectl on Ubuntu to create a local Kubernetes cluster for development and testing.

🐳 Step 1: Install Docker
Docker is required to run Kubernetes nodes as containers.
sudo apt update
sudo apt upgrade
sudo apt install -y docker.io

▶️ Verify Installation
docker --version
sudo usermod -aG docker $USER
newgrp docker


⚙️ Step 2: Install KIND (Kubernetes in Docker)

KIND allows you to run Kubernetes clusters using Docker containers.

# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64

# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-arm64

chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

▶️ Verify Installation
kind --version


☸️ Step 3: Install kubectl

kubectl is the Kubernetes CLI tool used to interact with clusters.

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl
sudo mv kubectl /usr/local/bin/kubectl

▶️ Verify Installation
kubectl version

mkdir kubernetes
cd kubernetes
vim kind-config.yml

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: quantum-cluster

nodes:
- role: control-plane
  image: kindest/node:v1.35.0

- role: worker
  image: kindest/node:v1.35.0

- role: worker
  image: kindest/node:v1.35.0
  
  :wq

  🎯 Next Step: Create KIND Cluster
  kind create cluster --name kind-config.yml
  kubectl get nodes

  💡 Notes
Docker must be running before creating the cluster
Ensure ports are open if using cloud VM (AWS, Azure, etc.)
KIND is best for local development and testing

🚀 Project Purpose

This project demonstrates:

Kubernetes local setup using KIND
Container-based cluster creation
DevOps workflow for learning and practice
