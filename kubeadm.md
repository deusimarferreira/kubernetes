# Kubeadm
Atualmente, o método mas direto para começar a construir um cluster real é usar o kubeadm, que surgiu na Kubernetes v1.4.0, e pode ser usado para iniciar um cluster rapidamente.

[Consulte a documentação](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

[Install Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

> swapoff -a

> https://stackoverflow.com/questions/53525975/kubernetes-error-uploading-crisocket-timed-out-waiting-for-the-condition


Para associar outros nós ao cluster, você precisará de pelo menos um token e um hash SHA256. Esta informação é retornada pelo comando ``kubeadm init`` e ``kubeadm join --token token head-node-IP``

~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com privilégios root, para isso use o comando sudo -i
sudo -i

# Find the IP address of the primary interface of the master server
ip addr show | grep inet
    ...
    inet 10.10.0.5/16 brd 10.10.255.255 scope global eth0

# Adiciona host no arquivo /etc/hosts
vim /etc/hosts
    10.10.0.5 k8smaster

# Criando nosso primeiro arquivo de configuração, necessário para inciar nosso primeiro cluster
# O conteúdo para o arquivo vc encontra neste repositório em ./yaml/kubeadm-config.yaml
vim kubeadm-config.yaml

# kubeadm init --dry-run
kubeadm init --config=kubeadm-config.yaml --upload-certs \
| tee kubeadm-init.out # Salva saida para revisitação futura

# Workers nodes
kubeadm join --token token head-node-IP # workers nodes
    ...
    
# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su
exit
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
~~~ 
