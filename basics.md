# Kubernetes
Kubernetes é um conjunto de daemons/binaries:
* [kubeadm (bootstrap a minimum viable Kubernetes cluster)](/kubeadm.md)
* [kube-apiserver (AKA the master)](/kube-apiserver.md)
* [kubelet (start/stop containers, sync conf](/kubelet.md)
* kube-scheduler (resources manager)
* kube-controller-manager (monitor RC, and maintain the desired state)
* kube-proxy (expose services on each node)
* [kubectl (CLI)](/kubectl.md)

## O que é Kubernets?
Kubernetes foi inspirado no projeto Borg (Sistema interno usado para gerenciar aplicações com Gmail, Apps, GCE).

Kubenetes carrega 15 anos de experiência do Google.

Devido a dificuldade de pronunciar o nome, muitos usam o nickname, K8s (Kate's), onde 8 é o número de letras da palavra Kuberbetes.

### Objetivos
* Container Orchestrator
* Workload Placement
* Infrastructure Abstraction
* Disered State

### Benfícios
* Speed of deployment
* Ability to absorb change quickly
* Ability to recovery quickly
* Hide complexity in the cluster

### Princípios
* Desired State (Declaritive Configuration) 
* Controllers (Control Loops)
* One Master (The API Server)

### Kubernetes Objects
* Pods
* Controllers
* Services
* Storage

## Concorrentes
* Docker Swarm
* Apache Mesos
* Nomad
* Rancher

## Recomendações de conteúdo
* [Borg paper](https://ai.google/research/pubs/pub43438)
* [Podcast Google](https://www.gcppodcast.com/post/episode-46-borg-and-k8s-with-john-wilkes/)
* [Kubernetes community hangout](https://github.com/kubernetes/community)
* #kubernetes-users [Slack](https://slack.kubernetes.io/)
* [Stack Overflow](https://stackoverflow.com/search?q=kubernetes)
* [Cloud Native](https://www.slideshare.net/chipchilders/cloud-foundry-the-platform-for-forging-cloud-native-applications)
