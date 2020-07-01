# Nodes
* Kubelet (10250)
    * Monitors API Server for changes
    * Responsible for Pod Lifecycle
    * Reports Node & Pod state
    * Pod liveness probes
* Kube-proxy
    * Network proxy iptables
    * Implements Services
    * Routing Traffic to Pods
    * Load Balancing
* Container Runtime
    * Downloads images and run containers
    * Container Runtime Interface
    * Docker
    * Many others ...

[Clique aqui](https://kubernetes.io/docs/concepts/architecture/nodes/) para mais informações.
