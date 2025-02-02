
### kube-apiserver
| #kube-apiserver-tag<br>^kube-apiserver-tag |
| ------------------------------------------ |
| [[kube-apiserver\|more]]                   |

The API server is the front end for the Kubernetes control plane.

### etcd
| #kube-etcd-tag<br>^kube-etcd-tag |
| -------------------------------- |
| [[etcd\|more]]                   |

Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.


### kube-scheduler
| #kube-scheduler-tag<br>^kube-scheduler-tag |
| ------------------------------------------ |
| [[kube-scheduler\|more]]                   |

Kube-sheduler watches for newly created Pods with no assigned 
node, and selects a node for them to run on.


### kube-controller-manager

| #kube-controller-manager-tag<br>^kube-controller-manager-tag |
| ------------------------------------------------------------ |
| [[kube-contoller-manager\|more]]                             |

Control plane component that runs controller processes.


### cloud-controller-manager
| #cloud-controller-manager-tag<br>^cloud-controller-manager-tag |
| -------------------------------------------------------------- |
| [[cloud-controller-manager\|more]]                             |

A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.


### kubelet
| #kubelet-tag<br>^kubelet-tag |
| ---------------------------- |
| [[kubelet\|more]]            |

An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.


### kube-proxy (optional)
| #kube-proxy-tag<br>^kube-proxy-tag |
| ---------------------------------- |
| [[kube-proxy\|more]]               |
kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.


### container runtime
| #container-runtime-tag<br>^container-runtime-tag |
| ------------------------------------------------ |
| [[container runtime\|more]]                      |

A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.

CRI Runtimes:
- cri-o
- rktlet
- frakti
- cri-containerd
- singularity-cri

### addon components

| #addon-components-tag<br>^addon-components-tag |
| ---------------------------------------------- |
| [[addon components\|more]]                     |

