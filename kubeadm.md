# Kubeadm
Atualmente, o método mas direto para começar a construir um cluster real é usar o kubeadm, que surgiu na Kubernetes v1.4.0, e pode ser usado para iniciar um cluster rapidamente.

Embora você possa executar todos os componentes como daemons/binaries, também pode executar o API server, o scheduler, e o controller-manager como contêineres. É isso que o ``kubeadm`` faz.

[Consulte a documentação](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

[Install Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

> swapoff -a

> https://stackoverflow.com/questions/53525975/kubernetes-error-uploading-crisocket-timed-out-waiting-for-the-condition


Para associar outros nós ao cluster, você precisará de pelo menos um token e um hash SHA256. Esta informação é retornada pelo comando ``kubeadm init`` e ``kubeadm join --token token head-node-IP``

~~~sh
# kubeadm init --dry-run
kubeadm init
kubeadm join --token token head-node-IP # workers nodes

kubeadm init --config=kubeadm-config.yaml --upload-certs \
    | tee kubeadm-init.out
~~~