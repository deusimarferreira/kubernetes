# Worker Node

## Instalação/Configuração
Os passos apresentados a seguir leva em consideração que você já tenha o **k8s tools** devidamente instaladas, caso contrário favor realizar [instalação k8s tools](/install.md)

### Ações no node master
~~~sh
ip addr show | grep inet

vim /etc/hosts
167.172.121.160 k8smaster

# Lista tokens existentes
sudo kubeadm token list
~~~

~~~sh
# Cria novo token
$ sudo kubeadm token create
d35xpy.1hwrqqwwr062jgqk
~~~

~~~sh
# Gera token-ca-cert-hash-sha256
openssl x509 -pubkey \
    -in /etc/kubernetes/pki/ca.crt | openssl rsa \
    -pubin -outform der 2>/dev/null | openssl dgst \
    -sha256 -hex | sed 's/^.* //'
80684ceaba35b55849fc2ec93a32c3e73f6956c56c50a120fd06c844e612f6bb
~~~

### Ações no node worker
~~~sh
# Join node worker
sudo su
kubeadm join \
    --token d35xpy.1hwrqqwwr062jgqk \
    k8smaster:6443 \
    --discovery-token-ca-cert-hash \
    sha256:80684ceaba35b55849fc2ec93a32c3e73f6956c56c50a120fd06c844e612f6bb

Then you can join any number of worker nodes by running the following on each as root:

kubectl -n kube-system get cm kubeadm-config -oyaml
kubeadm join k8smaster:6443 --token 5rn0dh.z96ii10l9bkww3ws \
    --discovery-token-ca-cert-hash sha256:20bdf9fd1da245bdce3000735c119f28ae5831c6a28a42a541ef90ab6e461117 
~~~