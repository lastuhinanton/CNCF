| #addon-components-page-tag<br>^addon-components-page-tag |
| -------------------------------------------------------- |
| [[K8s fundamentals#^addon-components-tag\|back]]         |

Following are some of the popular addon components that you might need on a cluster.

1. **CNI Plugin (Container Network Interface)**
2. **CoreDNS (For DNS server):** CoreDNS acts as a DNS server within the Kubernetes cluster. By enabling this addon, you can enable DNS-based service discovery.
3. **Metrics Server (For Resource Metrics):** This addon helps you collect performance data and resource usage of Nodes and pods in the cluster.
4. **Web UI (Kubernetes Dashboard):** This addon enables the Kubernetes dashboard to manage the object via web UI.

### CNI plugin:

How does the CNI Plugin work with Kubernetes?

1. The Kube-controller-manager is responsible for assigning pod CIDR to each node. Each pod gets a unique IP address from the pod CIDR.
2. Kubelet interacts with container runtime to launch the scheduled pod. The CRI plugin which is part of the Container runtime interacts with the CNI plugin to configure the pod network.
3. CNI Plugin enables networking between pods spread across the same or different nodes using an overlay network.

[![Kubernetes CNI Plugin workflow](https://devopscube.com/wp-content/uploads/2023/01/image-18.png)](https://devopscube.com/wp-content/uploads/2023/01/image-18.png)
Some popular CNI plugins include:
1. Calico
2. Flannel
3. Weave Net
4. Cilium (Uses eBPF)
5. Amazon VPC CNI (For AWS VPC)
6. Azure CNI (For Azure Virtual network)Kubernetes networking is a big topic and it differs based on the hosting platforms.


When it comes to networking, the following Kubernetes objects plays a key role.

1. Services
2. Ingress
3. Network policies.

Also, Kubernetes is extendable using CRDs, and Custom Controllers. So the cluster components also manage the objects created using custom controllers and custom resource definitions.