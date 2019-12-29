# Instalação

~~~sh
#Setup 
#   1. 3 VMs Ubuntu 16.04.5 or 18.04.1.0, 1 master, 2 nodes.
#   2. Static IPs on individual VMs
#   3. /etc/hosts hosts file includes name to IP mappings for VMs
#   4. Swap is disabled
#   5. Take snapshots prior to installations, this way you can install 
#       and revert to snapshot if needed

#Disable swap, swapoff then edit your fstab removing any entry for swap partitions
#You can recover the space with fdisk. You may want to reboot to ensure your config is ok. 
swapoff -a
vi /etc/fstab

sudo -i

apt-get update && apt-get upgrade -y

apt-get install -y docker.io

apt-get install -y vim

#Add the Kubernetes apt repository
vim /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
# Ou
bash -c 'cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF'

#Add Google's apt repository gpg key
curl -s \
    https://packages.cloud.google.com/apt/doc/apt-key.gpg \
    | apt-key add -

#Update the package list and use apt-cache to inspect versions available in the repository
apt-get update
apt-cache policy kubelet | head -n 20 
apt-cache policy docker.io | head -n 20 

#Install the required packages, if needed we can request a specific version
apt-get install -y \
kubeadm=1.16.1-00 kubelet=1.16.1-00 kubectl=1.16.1-00

apt-mark hold kubelet kubeadm kubectl

#Check the status of our kubelet and our container runtime, docker.
#The kubelet will enter a crashloop until it's joined. 
systemctl status kubelet.service 
systemctl status docker.service 

#Ensure both are set to start when the system starts up.
systemctl enable kubelet.service
systemctl enable docker.service

##
adduser student

vim /etc/sudoers.d/student
student ALL=(ALL) ALL

chmod 440 /etc/sudoers.d/student

.bashrc
PATH=$PATH:/usr/sbin:/sbin
~~~

## Erros
https://stackoverflow.com/questions/37227349/unable-to-start-docker-service-in-ubuntu-16-04/37640824