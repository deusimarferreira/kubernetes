# Master - Control Plane Components

* API Server (6443)
    * Central
    * Simple
    * RESTful
    * Updates etcd
* Cluster Store 
    * Persists State
    * key-value
    * etcd (2379-2380)
    * watch
* Scheduler (10251)
    * Watches API server
    * Schedulers PODs
    * Resources
    * Respects contraints
* Controller Manger (10252)
    * Controllers loops
    * Lifecycle functions and desired state
    * Watch and update the API Server
    * ReplicaSet