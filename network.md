# Pod Network
Antes de inicializar o cluster Kubernetes, a rede deve ser considerada para evitar os conflitos de IP. Existem várias opções de Pod Network, em vários níveis de desenvolvimento e feature.

* Calico - Usada em produção com software tais como Kubernetes, OpenShift, Docker Mesos e OpenStack.
* Flannel - Layer 3 IPV4 network entre os nodes e o cluster. Desenvolvida por CoreOS.
* Kube-router
* Romana
* Weave Net