
| #kube-etcd-page-tag<br>^kube-etcd-page-tag |
| ------------------------------------------ |
| [[K8s fundamentals#^kube-etcd-tag\|back]]  |

Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

[etcd](https://github.com/etcd-io/etcd) is an open-source strongly consistent, distributed key-value store. So what does it mean?

1. **Strongly consistent:** If an update is made to a node, strong consistency will ensure it gets updated to all the other nodes in the cluster immediately. Also if you look at [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), achieving 100% availability with strong consistency and & Partition Tolerance is impossible.
2. **Distributed**: etcd is designed to run on multiple nodes as a cluster without sacrificing consistency.
3. **Key Value Store:** A nonrelational database that stores data as keys and values. It also exposes a key-value API. The datastore is built on top of [BboltDB](https://github.com/etcd-io/bbolt) which is a fork of BoltDB.

When you use kubectl to get kubernetes object details, you are getting it from etcd. Also, when you deploy an object like a pod, an entry gets created in etcd.

In a nutshell, here is what you need to know about etcd.

1. etcd stores all configurations, states, and metadata of Kubernetes objects (pods, secrets, daemonsets, [deployments](https://devopscube.com/kubernetes-deployment-tutorial/), configmaps, statefulsets, etc).
2. `etcd` allows a client to subscribe to events using `Watch()` API . Kubernetes api-server uses the etcd’s watch functionality to track the change in the state of an object.
3. etcd exposes key-value API [using gRPC](https://etcd.io/docs/v3.5/learning/api/). Also, the [gRPC gateway](https://etcd.io/docs/v3.3/dev-guide/api_grpc_gateway/) is a RESTful proxy that translates all the HTTP API calls into gRPC messages. This makes it an ideal database for Kubernetes.
4. etcd stores all objects under the **/registry** directory key in key-value format. For example, information on a pod named Nginx in the default namespace can be found under **/registry/pods/default/nginx**

[![kubernetes etcd](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-etcd.gif)](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-etcd.gif)






