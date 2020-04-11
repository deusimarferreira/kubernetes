# Worker Node

## Instalação/Configuração Básicas
Os passos apresentados a seguir leva em consideração que você já tenha o **K8s tools** devidamente instaladas, caso contrário favor realizar [instalação K8s tools](/install.md)

## Instalação/Configuração Worker Node
### Ações no Master - Control Plane
~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su
ip addr show | grep inet

# Lista tokens existentes type "authe ..."
sudo kubeadm token list

# O token tem validade de 2 horas, caso todos estejam expirados, gere um novo token
sudo kubeadm token create

# Crie e use um token CA Cert Hash no master para garantir que o join entre o node e o cluster seja realizado de maneira segura.
# Gera token-ca-cert-hash-sha256
# Você receberá uma string como resultado.
openssl x509 -pubkey \
    -in /etc/kubernetes/pki/ca.crt | openssl rsa \
    -pubin -outform der 2>/dev/null | openssl dgst \
    -sha256 -hex | sed 's/^.* //'
#> saída: 5ec5dee725c7c06a93f59bf180ba862e101d99fe321930d0653267d47b29e5a9
~~~

### Ações no Worker Node (this)
~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com privilégios root, para isso use o comando sudo -i
sudo -i

# Adiciona host no arquivo /etc/hosts
vim /etc/hosts
    10.10.0.5 k8smaster

# Join node worker
kubeadm join \
    --token p1oki4.k5v3q3njj8dfb9ce \
    k8smaster:6443 \
    --discovery-token-ca-cert-hash \
    sha256:5ec5dee725c7c06a93f59bf180ba862e101d99fe321930d0653267d47b29e5a9

# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su
# Os comandos a seguir devem falhar. Você não possui o cluster or authentication keys no arquivo .kube/config
exit
kubectl get nodes
    The connection to the server localhost:8080 was refused - did you specify the right host or port?

ls -l .kube
    cannot access '.kube': No such file or directory
~~~