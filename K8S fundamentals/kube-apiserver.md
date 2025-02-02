
| #kube-apiserver-page-tag<br>^kube-apiserver-page-tag |
| ---------------------------------------------------- |
| [[K8s fundamentals#^kube-apiserver-tag\|back]]       |

kube-apiserver is designed to scale horizontally—that is, it scales by deploying more instances. You can run several instances of kube-apiserver and balance traffic between those instances.
### Kubernetes API Aggregation Layer
The aggregation layer allows Kubernetes to be extended with additional APIs, beyond what is offered by the core Kubernetes APIs. The additional APIs can either be ready-made solutions such as a metrics server, or APIs that you develop yourself.

### Kubernetes api-server is responsible for:

1. **API management**: Exposes the cluster API endpoint and handles all API requests. The API is version and itsupports multiple API versions simultaneously.
2. **Authentication** (Using client certificates, bearer tokens, and HTTP Basic Authentication) and **Authorization** (ABAC and RBAC evaluation)
3. Processing API requests and validating data for the API objects like pods, services, etc. (Validation and Mutation Admission controllers)
4. api-server coordinates all the processes between the control plane and worker node components.
5. API server also contianes an [aggreagation layer](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/apiserver-aggregation/) which allows you to extend Kubernetes API to create custom APIs resources and controllers.
6. The only component that the **kube-apiserver initiates a connection to** is the **etcd** component. All the other components connect to the API server.
7. The API server also **supports watching resources** for changes. For example, clients can establish a watch on specific resources and receive real-time notifications when those resources are created, modified, or deleted.
8. Each component (Kubelet, scheduler, controllers) **independently watches the API server** to figure out what it needs to do.








