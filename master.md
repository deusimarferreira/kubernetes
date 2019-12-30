# Master - Control Plane Components
* API Server (6443)
    * Central
    * Simple
    * RESTful
    * Updates etcd
* Cluster Store 
    * Persists State
    * key-value
    * etcd (2379-2380)
    * watch
* Scheduler (10251)
    * Watches API server
    * Schedulers PODs
    * Resources
    * Respects contraints
* Controller Manger (10252)
    * Controllers loops
    * Lifecycle functions and desired state
    * Watch and update the API Server
    * ReplicaSet

## Instalação/Configuração
Os passos apresentados a seguir leva em consideração que você já tenha o **k8s tools** devidamente instaladas, caso contrário favor realizar [instalação k8s tools](/install.md)

ip addr show | grep inet

vim /etc/hosts
vim kubeadm-config.yaml

kubeadm init --config=kubeadm-config.yaml --upload-certs \
| tee kubeadm-init.out # Save output for future review

~~~sh
# Os comandos a seguir são realizado com usuário não root/su
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

wget https://tinyurl.com/yb4xturm -O rbac-kdd.yaml
wget https://tinyurl.com/y2vqsobb -O calico.yaml
~~~ 

### Network
Mais informações acesse [network](/network.md)
~~~sh
kubectl apply -f rbac-kdd.yaml
kubectl apply -f calico.yaml
~~~

~~~sh
kubectl taint nodes \
    --all node-role.kubernetes.io/master-

kubectl taint nodes \
    --all node.kubernetes.io/not-ready-
~~~
