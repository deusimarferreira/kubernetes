# Minikube

## Instalação
Para informações sobre instalação acesse [Install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)

## Iniciando Cluster com Minikube
~~~sh
# Windows
$ minikube start --driver=hyperv
~~~

## Explorando comando kubectl

~~~sh
# Vamos verificar os nodes existentes
$ kubectl get nodes

# Recupera os pods no namespace kube-system
$ kubectl get pods --namespace=kube-system

# Deploy do nginx
$ kubectl create deployment nginx --image=nginx

# Expondo serviço
$ kubectl expose deployment nginx --port=80

# Listando serviço
$ kubectl get svc nginx

# Recuperar IP+PORT da aplicação
$ minikube service nginx --url
~~~
