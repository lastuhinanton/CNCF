
| #kube-scheduler-page-tag<br>^kube-scheduler-page-tag |
| ---------------------------------------------------- |
| [[K8s fundamentals#^kube-scheduler-tag\|back]]       |

Factors taken into account for scheduling decisions include: individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines

The following image shows a high-level overview of **how the scheduler works**.

[![Kubernetes Scheduler](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-sc.gif)](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-sc.gif)

Here is how the scheduler works.

1. To choose the best node, the Kube-scheduler uses **filtering and scoring** operations.
2. In **filtering**, the scheduler finds the best-suited nodes where the pod can be scheduled. For example, if there are five worker nodes with resource availability to run the pod, it selects all five nodes. If there are no nodes, then the pod is unschedulable and moved to the scheduling queue. If It is a large cluster, let’s say 100 worker nodes, and the scheduler doesn’t iterate over all the nodes. There is a scheduler configuration parameter called `**percentageOfNodesToScore**`. The default value is typically **50%**. So it tries to iterate over 50% of nodes in a round-robin fashion. If the worker nodes are spread across multiple zones, then the scheduler iterates over nodes in different zones. For very large clusters the default `**percentageOfNodesToScore**` is 5%.
3. In the **scoring phase**, the scheduler ranks the nodes by assigning a score to the filtered worker nodes. The scheduler makes the scoring by calling multiple [scheduling plugins](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins). Finally, the worker node with the highest rank will be selected for scheduling the pod. If all the nodes have the same rank, a node will be selected at random.
4. Once the node is selected, the scheduler creates a binding event in the API server. Meaning an event to bind a pod and node.

[![How Kubernetes Scheduler chooses a Node](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-sc-logic.gif)](https://devopscube.com/wp-content/uploads/2024/04/02-k8s-architecture-sc-logic.gif)









