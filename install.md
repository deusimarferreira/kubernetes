# Instalação

## kubectl
https://kubernetes.io/docs/tasks/tools/install-kubectl/

## Minikube
https://kubernetes.io/docs/tasks/tools/install-minikube/

```sh
minikube start --vm-driver='none'

kubeadm init
kubeadm join --token token head-node-IP

docker rm -f $(docker ps -aq) \
& rm -rf /var/lib/etcd \
& rm -rf /etc/kubernetes/
netstat -tlpn | grep 10250

swapoff -a

kubeadm init --dry-run

https://stackoverflow.com/questions/53525975/kubernetes-error-uploading-crisocket-timed-out-waiting-for-the-condition

kubectl create -f https://git.io/weave-kube
```