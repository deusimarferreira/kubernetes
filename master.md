# Master - Control Plane
O Master executa varios servers e gerenciamento processos para o cluster, ele é responsável por manter toda a sinfonia dentro do cluster. 

## Componentes
* Kube API Server (6443)
    * Central
    * Simple
    * RESTful
    * Updates etcd
* Kube Cluster Store 
    * Persists State
    * key-value
    * etcd (2379-2380)
    * watch
* Kube Scheduler (10251)
    * Watches API server
    * Schedulers PODs
    * Resources
    * Respects contraints
* Kube Controller Manager (10252)
    * Controllers loops
    * Lifecycle functions and desired state
    * Watch and update the API Server
    * ReplicaSet
* Kube Cloud Controller Manager (Optional agent)

## Instalação/Configuração Básicas
Os passos apresentados a seguir leva em consideração que você já tenha o **K8s tools** devidamente instaladas, caso contrário favor realizar [instalação K8s tools](/install.md)

### Kubeadm
[Clique aqui](/kubeadm.md)

### Minikube
[Clique aqui](/minikube.md)

## Network
Mais informações acesse [Network](/network.md)

~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su

# Realize o download dos arquivos para configurar a rede usando o plugin calico
# Links:
# https://docs.projectcalico.org/v3.3/getting-started/kubernetes/installation/hosted/rbac-kdd.yaml
# https://docs.projectcalico.org/v3.9/manifests/calico.yaml
wget https://tinyurl.com/yb4xturm -O rbac-kdd.yaml
wget https://tinyurl.com/y2vqsobb -O calico.yaml

kubectl apply -f rbac-kdd.yaml
kubectl apply -f calico.yaml
~~~

> Dica: durante todo processo de administração do cluster iremos precisar usar muitas vezes os comandos do kubectl, para facilitar vamos adicionar bash-completion para posibilitar o auto-complete usando a tecla <Tab>

~~~sh
# Instalação e configuração do auto-complete
sudo apt-get install bash-completion -y
source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc

# Teste o auto-complete
kubectl des<Tab> n<Tab><Tab>
~~~
