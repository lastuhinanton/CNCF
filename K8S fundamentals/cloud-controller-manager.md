
| #cloud-controller-manager-page-tag<br>^cloud-controller-manager-page-tag |
| ------------------------------------------------------------------------ |
| [[K8s fundamentals#^cloud-controller-manager-tag\|back]]                 |

[Cloud controller integration](https://devopscube.com/aws-cloud-controller-manager/) allows Kubernetes cluster to provision cloud resources like instances (for nodes), Load Balancers (for services), and Storage Volumes (for persistent volumes).

[![Kubernetes Cloud Controller Manager (CCM)](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-ccm-1.gif)](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-ccm-1.gif)

Three main controllers that are part of the cloud controller manager.
1. **Node controller:** This controller updates node-related information by talking to the cloud provider API. For example, node labeling & annotation, getting hostname, CPU & memory availability, nodes health, etc.
2. **Route controller:** It is responsible for configuring networking routes on a cloud platform. So that pods in different nodes can talk to each other.
3. **Service controller**: It takes care of deploying load balancers for kubernetes services, assigning IP addresses, etc.

