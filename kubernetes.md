Kubernetes the hard way:
- Setup compute resources using vagrant
- Installed client tools like kubectl 
- Provision certificate    - Generate certificate authority and store it on master  - Generate admin certs for master using the previously generated ca cert  - controller-manager certificates  - kube-proxy certificates  - kube scheduler certs  - kube-apiserver certs : where we need to notify all components may reach kibe-api server like master servers, load balancers  - etcd certificates: this should also have addresses of all servers  - service-account certs  Next these were distributed ca, kube-apiserver, service-account (to generate and issue tokens), etcd
- Generate kibe-config files for authentications of individual components i.e. cube-proxy, kube-controller-manager, kube-schedular, admin kube-config and distribute them accordingly 
- Data encryption file for master
- Setup etcd cluster by first downloading binary, then creating etc service file  where we tell all the certs and keys 
- Kube control plane: kube-apiserver, kube-controller-manager, kube-scheduler, kubectl : for master, similar to etcd after downloading binaries, create service yamls 
- Setup load balancer using haproxy (on load balancer node)
- Setup worker node:  - generate cert for node authorization   - kube-config file  - kube-config file  - from master copy certs to worker 1 and install kubectl, kube-proxy and kubelet on node  - configure kubelet -config and kubelet service, cube-proxy-config and cube-proxy service 
- TLS bootstrap node which allows node to creates its own cert and register with master
- Pod networking using CNI plugin from weave works
- Next create cluster roles and cluster role binding for kube-apiserver to perform actions on nodes
- Install core-dns for dns based service discovery 
