# Instalação
A seguir serão apresentados os procedimentos para realizar a instalação dos daemons/binaries necessários para trabalhar com K8s.

## Pré-requisitos
Todos os execícios foram realizados na distribuição Linux Ubuntu versão 18.04.

~~~sh
# Para nosso cenário de estudos vamos precisar criar usuario student e adiciona-lo com permissão sudoers
adduser student
echo 'student ALL=(ALL) ALL' >> /etc/sudoers.d/student
chmod 440 /etc/sudoers.d/student

# Saia do root shell
exit

# Sugiro que você adicione o contéudo (PATH=$PATH:/usr/sbin:/sbin) no arquivo .bashrc no diretório inicial
vim .bashrc
PATH=$PATH:/usr/sbin:/sbin
~~~

## Vamos para Instalação
A seguir apresento todos os comandos necessários para realizar as devidas instalação, informações sobre cada comando poderá ser verificada em seus respectivos comentários.

~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com privilégios root, para isso use o comando sudo -i
sudo -i

# Agora vamos realizar a atualização do servidor
apt-get update && apt-get upgrade -y

# Vamos utilizar o vim para editar os arquivos necessários, caso não tenha instalado, realize sua instalação
apt-get install -y vim

# Certifique-se que o swap esteja desabilitado.
# Essa ação pode ser falcilmente realizada usando o comando swapoff, que remove do fstab todas entradas para partições de swap
swapoff -a
vim /etc/fstab

# Para realizar a instalação dos binários K8s será necessário adicionar o repositório (apt repository)
# Existe duas maneiras para isso, que são:
# Exemplo 1 - criar o arquivo usando comando echo e adicionar o conteúdo (deb http://apt.kubernetes.io/ kubernetes-xenial main)
echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' >> /etc/apt/sources.list.d/kubernetes.list

# Exemplo 2 - ou usar o comando bash option -C
bash -c 'cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF'

# Adicionar repositório Google (apt repository gpg key)
curl -s \
    https://packages.cloud.google.com/apt/doc/apt-key.gpg \
    | apt-key add -

# Atualiza a lista de pacotes (package list) e use o apt-cache para inspecionar as versões disponíveis no repositório adicionado
apt-get update
apt-cache policy kubelet | head -n 20 
apt-cache policy docker.io | head -n 20 

# Instalação do container runtime, que em nosso caso será Docker 
apt-get install -y docker.io

# Intalação do pacotes requeridos, se necessario podemos especificar a versão desejada, como a vesão atualmente 
# utilizada para certificação CKA é Kubernetes v1.17 iremos utilizar essa versão
apt-get install -y \
kubeadm=1.17.4-00 kubelet=1.17.4-00 kubectl=1.17.4-00

# Vamos usar o comando apt-mark para previnir que o pacote seja automaticamente instalado, actualizado ou removido
# mais informações sobre o comando acesse http://manpages.ubuntu.com/manpages/trusty/pt/man8/apt-mark.8.html
apt-mark hold kubelet kubeadm kubectl docker

# Chacar o status de nosso kubelet e container runtime, docker.
# The kubelet will enter a crashloop until it's joined. 
systemctl status kubelet.service 
systemctl status docker.service 

# Certifique que ambos estejam configurados para iniciar quando o So for iniciado.
systemctl enable kubelet.service
systemctl enable docker.service
~~~

## Erros
https://stackoverflow.com/questions/37227349/unable-to-start-docker-service-in-ubuntu-16-04/37640824