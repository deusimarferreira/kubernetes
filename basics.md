# Kubernetes
Nesta sessão você encontrará alguns conceitos básicos que são extremamente importantes para entendimento do funcionamento do K8s.

## O que é Kubernetes?
O Kubernetes é uma plataforma portátil, extensível, open-source para gerenciar worloads (cargas de trabalho) e services (serviços) executados em containers (contêineres), que facilita a configuração declarativa e a automação. Possui amplo ecossistema que permite uma rápida expansão (vertifcal e/ou horizontal). Os serviços, suporte e ferramentas do Kubernetes estão amplamente disponíveis.

* Objetivos
    * Container Orchestrator
    * Workload Placement
    * Infrastructure Abstraction
    * Desired State [ref.](https://medium.com/@yannalbou/kubernetes-desired-state-4c5c4e873743)
* Benfícios
    * Speed of deployment
    * Ability to absorb change quickly
    * Ability to recovery quickly
    * Hide complexity in the cluster
* Princípios
    * Desired State (Declaritive Configuration) 
    * Controllers (Control Loops)
    * One Master (The API Server)

[Clique aqui](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) para mais informações.

## Componentes Kubernetes
Um cluster Kubernetes consiste nos componentes que representam o control plane (master) e um conjunto de máquinas chamadas de nodes.

![](https://d33wubrfki0l68.cloudfront.net/7016517375d10c702489167e704dcb99e570df85/7bb53/images/docs/components-of-kubernetes.png)From Kubernetes Docs

[Clique aqui](https://kubernetes.io/docs/concepts/overview/components/) para mais informações.

### Objetos Kubernetes [ref.](https://kubernetes.io/docs/concepts/#kubernetes-objects)
O Kubernetes possui abstrações que representam o estado do seu sistema: aplicativos e cargas de trabalho implantados em contêineres, seus recursos de rede e disco associados e outras informações sobre o que seu cluster está fazendo. Essas abstrações são representadas por objetos na Kubernetes API.

Os objetos basícos do Kubernetes inclue:

* Pod
    - Unidade mas básica de execução de um aplicativo
    - Menor e mais simples unidade do modelo de objetos do kate's
    - Efêmero (Ephemeral) - Nenhum Pod é "reimplantado"
    - Um ou mais contâineres
    - Encapsula o contêiner de um aplicativo (ou vários contêineres), recursos de armazenamento, um IP de rede exclusivo e opções que determinam como o contêiner deve ser executado.
    - Docker é o runtime mais comun em um Pod Kate's, mas é possível utilizar outros runtimes existentes, ficou curiso [veja outros runtimes aqui](https://github.com/deusimarferreira/containers/blob/master/containers-runtimes.md).
    - O trabalho do Kate's é manter o Pod em funcionamento, mais especificamente, mantendo o estado desejado (Desired State).
        * State
        * Health
* Controller
    - Cria e gerenciar seus Pods
    - Define o estado desejado (Desired State)
    - Responde o estado (state) e a saúde (health) para o Pod
    - ReplicaSet - Define o número de réplicas
    - Deployment - Gerencia o rollout do ReplicaSet
* Service
    - Uma abstração que define um conjunto lógico de Pods e sua política de acesso (às vezes esse pattern é chamado de microsserviço), em linhas gerais, é uma abstração da camada de rede para permitir acesso ao Pod.
    - Balanceamento de carga (Load balancing)
    - Escalonamento por adição/remoção de Pods
    - Adiciona persistência para o universo efêmero
* Volume
    - Abstração responsável por possibilitar armazenamento compartilhado
        * PersistentVolume (PV)
        * PersistentVolumeClaim (PVC)
* Namespace
    - Clusters virtuais num mesmo cluster físico
    - Destinam-se ao uso em ambientes com muitos usuários espalhados por várias equipes ou projetos

O Kubernetes também contém abstrações de alto nível que dependem dos [Controllers]() para criar os objetos básicos e fornecer funcionalidades adicionais e features de conveniência. Esses incluem:

* Deployment
* DaemonSet
* StatefulSet
* ReplicaSet
* Job

## Concorrentes
* Docker Swarm
* Apache Mesos
* Nomad
* Rancher

# Recomendações de conteúdo
* [K8s Docs](https://kubernetes.io/docs/concepts/overview/)
* [Borg paper](https://research.google/pubs/pub43438/)
* [Podcast Google](https://www.gcppodcast.com/post/episode-46-borg-and-k8s-with-john-wilkes/)
* [Kubernetes community hangout](https://github.com/kubernetes/community)
* #kubernetes-users [Slack](https://slack.kubernetes.io/)
* [Stack Overflow](https://stackoverflow.com/search?q=kubernetes)
* [Cloud Native](https://www.slideshare.net/chipchilders/cloud-foundry-the-platform-for-forging-cloud-native-applications)
