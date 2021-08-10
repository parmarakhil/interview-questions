# Kubernetes

1. Kubernetes is an orchestration framework for docker containers which helps expose containers as services to the outside world
2. Kubernetes helps manages services
￼
3.  Minion is the node on which all the services run. You can have many minions running at one point in time
4. Each minion will host one or more POD
5. Each POD can host a different set of docker containers.
6. Proxy is then used to control the exposing of these services to the outside world
7. Components of Kubernetes architecture
    1. etcd
        1. It is a highly available key-value store that is used for storing shared configuration and service discovery
        2. Applications will be able to connect to the services via the discovery service
    2. Flannel
        1. This is a backend network which is required for the containers
    3. Kube-apiserver
        1. This is an API which can be used to orchestrate the docker containers
    4. Kube-controller-manager
        1. This is used to control the Kubernetes-services
    5. Kube-scheduler
        1. This is used to schedules the containers on hosts
    6. Kubelet
        1. This is used to control the launching of containers via manifest files
    7. Kube-proxy
        1. This is used to provide network proxy services to the outside world
