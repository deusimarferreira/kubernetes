# Instalação

## Minikube
Para informações sobre instalação acesse [Install Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)

### Ubuntu 19.04
~~~sh
# Instalação das dependências
# https://tutorialforlinux.com/2019/03/30/step-by-step-kvm-ubuntu-19-04-installation-guide/2/
sudo apt update

# https://help.ubuntu.com/community/KVM/Installation
# libvirt-daemon
sudo apt-get install qemu qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils

sudo chown janaina:libvirt /dev/kvm
sudo chown janaina:libvirt /var/run/libvirt/libvirt-sock

rmmod kvm_intel
modprobe -a kvm_intel

# Para mais informações acesse https://minikube.sigs.k8s.io/docs/start/linux/
# https://bugzilla.redhat.com/show_bug.cgi?id=950436
minikube start --vm-driver=kvm2 -p villalabs
~~~

## Kubeadm
Atualmente, o método mas direto para começar a construir um cluster real é usar o kubeadm, que surgiu na Kubernetes v1.4.0, e pode ser usado para iniciar um cluster rapidamente.

[Consulte a documentação](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

[Install Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

> swapoff -a

> https://stackoverflow.com/questions/53525975/kubernetes-error-uploading-crisocket-timed-out-waiting-for-the-condition


Para associar outros nós ao cluster, você precisará de pelo menos um token e um hash SHA256. Esta informação é retornada pelo comando ``kubeadm init`` e ``kubeadm join --token token head-node-IP``

~~~sh
# kubeadm init --dry-run
kubeadm init
kubeadm join --token token head-node-IP # workers nodes
~~~

## Kubectl
https://kubernetes.io/docs/tasks/tools/install-kubectl/
~~~sh
# Criar uma rede com kubectl usando um resource manifest, no exemplo abaixo vamos usar o Weave network como exemplo. 

kubectl create -f https://git.io/weave-kube
~~~

~~~sh
# Removendo configs kubernetes
docker rm -f $(docker ps -aq) \
& rm -rf /var/lib/etcd \
& rm -rf /etc/kubernetes/
netstat -tlpn | grep 10250
~~~