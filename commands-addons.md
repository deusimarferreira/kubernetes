# Commands Add-ons

## Master - Control Plane
### Consultando Informações do Cluster
~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su

kubectl get nodes

# Veja os detalhes do node, considere dedicar um pouco de tempo para analisar cada linha
# O master não permitirá pods que não sejam de infraestrutura por padrão por motivos de segurança e contenção de recursos.
kubectl describe node ubuntu-s-1vcpu-1gb-nyc1-01

# Determine if the DNS and Calico pods are ready for use. They should all show a status of Running. It may take a minute or two to transition from Pending.
kubectl get pods --all-namespaces

NAMESPACE       NAME                        READY   STATUS              RESTARTS    AGE
kube-system     calico-node-qkvzh           2/2     Running             0           59m
kube-system     calico-node-vndn7           2/2     Running             0           12m
kube-system     coredns-576cbf47c7-rn6v4    0/1     ContainerCreating   0           3s
kube-system     coredns-576cbf47c7-vq5dz    0/1     ContainerCreating   0           94m

# Se o retorno do comando acima estive "ContainerCreating" para "coredns-" você pode remover os pods para que eles sejam recriados pelo cluster K8s
kubectl -n kube-system delete \
    pod coredns-576cbf47c7-vq5dz coredns-576cbf47c7-rn6v4

# When it finished you should see a new tunnel, tunl0, interface. It may take up to a minute to be created. As you create objects more interfaces will be created, such as cali interfaces when you deploy pods, as shown in the output below.
ip a | grep tunl0 && ip a | grep cali
~~~

### Taints
By default, kubernetes cluster will not schedule pods on the master node for security reasons. But if we would like to be able to schedule pods on the master node, e.g: for a single-node kubernetes cluster for testing and development purposes, we can run “$ kubectl taint” command.

~~~sh
# Vamos permitir que nosso master execute non-infrastructure pods, mas esse passo deve ser pulado em ambiente de produção.
kubectl describe node | grep -i taint

# Note the minus sign (-) at the end, which is the syntax to remove a taint. As the second node does not
have the taint you will get a not found error.
kubectl taint nodes \
    --all node-role.kubernetes.io/master-

kubectl taint nodes \
    --all node.kubernetes.io/not-ready-
~~~