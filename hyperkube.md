# Hyperkube
Semelhante ao minikube, é um all-in-one binary, que está disponível em imagens de containers (e.g. gcr.io/google_containers/hyperkube:v1.10.12).

O projeto é mantido pelo Google, sendo necessário adicionar o reposítorio Docker para poder realizar o ``pull`` das imagens. [Hyperkube Registry](https://console.cloud.google.com/gcr/images/google-containers/GLOBAL/hyperkube)

## Instalação
Esse método de instalação consiste em executar o **kubelet** como um system daemon e configurá-lo para ler no manifests as definições de como executar os outros componentes (i.e. o API server, o scheduler, **etcd**, o controller). No nosso caso os manifests iremos utilizara imagem do **Hyperkube**. O **kubelet** ficará responsável em garantir que os containers sejam reiniciados caso morram.

Comandos para realizar o ``pull`` das imagens Docker.
~~~sh
$ docker run --rm gcr.io/google_containers/hyperkube:v1.15.5 /hyperkube apiserver --help 
$ docker run --rm gcr.io/google_containers/hyperkube:v1.15.5 /hyperkube scheduler --help 
$ docker run --rm gcr.io/google_containers/hyperkube:v1.15.5 /hyperkube controller-manager --help
~~~