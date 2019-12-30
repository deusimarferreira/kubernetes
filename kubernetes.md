# Kubernetes Source
A [lista de releases](https://github.com/kubernetes/kubernetes/releases) está disponível no Github, Junto com **gcloud**, **minikube** e **kubeadm**, eles abrangem vários cenários para começar a usar o Kubernetes.

* Realizar clone dos fontes via Github e compilar nativamente em sua plataforma via ``Makefile``
* Ou via iamgens Docker 

Para realizar a compilação via **make** você precisar de pelo menos 500MB de espaço em disco e Golang instalada em seu ambiente.
~~~sh
$ cd $GOPATH
$ git clone https://github.com/kubernetes/kubernetes.git
$ cd kubernetes
$ make
~~~
``_output/bin`` - Diretório onde os binários serão gerados 
