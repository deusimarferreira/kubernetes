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