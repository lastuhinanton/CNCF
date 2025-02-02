
| #kube-proxy-page-tag<br>^kube-proxy-page-tag |
| -------------------------------------------- |
| [[K8s fundamentals#^kube-proxy-tag\|back]]   |
kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

kube-proxy uses the operating system packet filtering layer if there is one and it's available. Otherwise, kube-proxy forwards the traffic itself.

If you use a network plugin that implements packet forwarding for Services by itself, and providing equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your cluster.

Kube-proxy is a daemon that runs on every node as a [daemonset](https://devopscube.com/kubernetes-daemonset/). It is a proxy component that implements the Kubernetes Services concept for pods. (single DNS for a set of pods with load balancing). It primarily proxies UDP, TCP, and SCTP and does not understand HTTP.

Kube-proxy then uses any one of the following modes to create/update rules for routing traffic to pods behind a Service

1. **[IPTables](https://wiki.centos.org/HowTos/Network/IPTables)**: It is the default mode. In IPTables mode, the traffic is handled by IPtable rules. This means that for each service, IPtable rules are created. These rules capture the traffic coming to the ClusterIP and then forward it to the backend pods. Also, In this mode, kube-proxy chooses the backend pod random for load balancing. Once the connection is established, the requests go to the same pod until the connection is terminated.
2. **[IPVS](https://en.wikipedia.org/wiki/IP_Virtual_Server):** For clusters with services exceeding 1000, IPVS offers performance improvement. It supports the following load-balancing algorithms for the backend.
    1. `rr`: round-robin : It is the default mode.
    2. `lc`: least connection (smallest number of open connections)
    3. `dh`: destination hashing
    4. `sh`: source hashing
    5. `sed`: shortest expected delay
    6. `nq`: never queue
[![how does kube proxy work - Workflow](https://devopscube.com/wp-content/uploads/2023/01/image-14-748x1024.png)](https://devopscube.com/wp-content/uploads/2023/01/image-14.png)
**1.29** **Alpha Feature:** Kubeproxy has a new 𝗻𝗳𝘁𝗮𝗯𝗹𝗲𝘀 based backend. nftables is the successor of IPtables that is Designed to be simpler and more efficient


