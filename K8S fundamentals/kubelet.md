
| #kubelet-page-tag<br>^kubelet-page-tag  |
| --------------------------------------- |
| [[K8s fundamentals#^kubelet-tag\|back]] |
Kubelet is an agent component that runs on every node in the cluster. t does not run as a container instead runs as a daemon, managed by systemd.

The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn't manage containers which were not created by Kubernetes.

kubelet is responsible for the following:
1. Creating, modifying, and deleting containers for the pod.
2. Responsible for handling liveliness, readiness, and startup probes.
3. Responsible for Mounting volumes by reading pod configuration and creating respective directories on the host for the volume mount.
4. Collecting and reporting Node and pod status via calls to the API server with implementations like `cAdvisor` and `CRI`.

Kubelet is also a controller that watches for pod changes and utilizes the node’s container runtime to pull images, run containers, etc.

Following are some of the key things about kubelet.
1. Kubelet uses the CRI (container runtime interface) gRPC interface to talk to the container runtime.
2. It also exposes an HTTP endpoint to stream logs and provides exec sessions for clients.
3. Uses the CSI (container storage interface) gRPC to configure block volumes.
4. It uses the CNI plugin configured in the cluster to allocate the pod IP address and set up any necessary network routes and firewall rules for the pod.

[![Kubernetes component kubelet explained](https://devopscube.com/wp-content/uploads/2023/01/kubelet-architecture-830x1024.png)](https://devopscube.com/wp-content/uploads/2023/01/kubelet-architecture.png)



