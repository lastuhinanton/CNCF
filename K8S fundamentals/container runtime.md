
| #container-runtime-page-tag<br>^container-runtime-page-tag |
| ---------------------------------------------------------- |
| [[K8s fundamentals#^container-runtime-tag\|back]]          |

[official doc](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md)

Container runtime runs on all the nodes in the Kubernetes cluster. It is responsible for pulling images from container registries, running containers, allocating and isolating resources for containers, and managing the entire lifecycle of a container on a host.

To understand this better, let’s take a look at two key concepts:

1. **Container Runtime Interface (CRI):** It is a set of APIs that allows Kubernetes to interact with different container runtimes. It allows different container runtimes to be used interchangeably with Kubernetes. The CRI defines the API for creating, starting, stopping, and deleting containers, as well as for managing images and container networks.
2. **Open Container Initiative (OCI):** It is a set of standards for container formats and runtimes


**Container Lifecycle Hooks**
Kubernetes supports post-start and pre-stop lifecycle hooks, with ongoing discussion for supporting pre-start and post-stop hooks in [#140](https://issues.k8s.io/140).

These lifecycle hooks will be implemented by Kubelet via `Exec` calls to the container runtime. This frees the runtimes from having to support hooks natively.

Illustration of the container lifecycle and hooks:
![[Pasted image 20250128193956.png]]

High-level overview of how container runtime works with kubernetes.
[![Kubernetes container runtime CRI-O overview](https://devopscube.com/wp-content/uploads/2022/12/image-5-1024x702.png)](https://devopscube.com/wp-content/uploads/2022/12/image-5.png)
**Definition:**
The **Container Runtime Interface (CRI)** is a plugin interface in Kubernetes that defines how the Kubernetes kubelet (the node agent) interacts with container runtimes. Essentially, it standardizes communication between Kubernetes and the underlying software that runs containers (such as Docker, containerd, or CRI-O).


#### Features:
1. Encrypted container images
2. Lazy Pulling
3. P2P image distribution
4. Image signing and verifying
5. Namespaces in K8s

