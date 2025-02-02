
| #kube-controller-manager-page-tag<br>^kube-controller-manager-page-tag |
| ---------------------------------------------------------------------- |
| [[K8s fundamentals#^kube-controller-manager-tag\|back]]                |

Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.

There are many different types of controllers. Some examples of them are:

- Node controller: Responsible  noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
- ServiceAccount controller: Create default ServiceAccounts for new namespaces.

**Kube controller manager** is a component that manages all the Kubernetes controllers. Kubernetes resources/objects like pods, namespaces, jobs, replicaset are managed by respective controllers. Also, the Kube scheduler is also a controller managed by the Kube controller manager.

[![Kube Controller Manager](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-cm.gif)](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-cm.gif)

Following is the list of important built-in Kubernetes controllers.
1. Deployment controller
2. Replicaset controller
3. DaemonSet controller 
4. Job Controller ([Kubernetes Jobs](https://devopscube.com/create-kubernetes-jobs-cron-jobs/))
5. CronJob Controller
6. endpoints controller
7. namespace controller
8. [service accounts](https://devopscube.com/kubernetes-api-access-service-account/) controller.
9. Node controller


Here is what you should know about the Kube controller manager.
1. It manages all the controllers and the controllers try to keep the cluster in the desired state.
2. You can extend kubernetes with **custom controllers** associated with a custom resource definition.





