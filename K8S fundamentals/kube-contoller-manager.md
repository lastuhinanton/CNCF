
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


#### **Deployment controller**

**Purpose**: Manages stateless applications (e.g., web servers) by ensuring a specified number of Pod replicas are running. Handles rolling updates, rollbacks, and scaling.  
**Key Use Case**: Stateless apps where Pods are interchangeable.
##### How It Works:

- Creates/updates **ReplicaSets** (which manage Pods).
    
- Enables zero-downtime deployments via rolling updates.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-server
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
        - name: nginx
          image: nginx:1.20
```




#### **StatefulSet Controller**

**Purpose**: Manages stateful applications (e.g., databases) with stable network identifiers, persistent storage, and ordered scaling.  
**Key Use Case**: Apps requiring unique identities (e.g., MySQL, Kafka).

##### How It Works:

- Assigns each Pod a unique ordinal index (e.g., `app-0`, `app-1`).
    
- Uses **PersistentVolumeClaims (PVCs)** for per-Pod storage.

StatefulSet (Manages Pods with Stable IDs)
│
├── Pod (mysql-0)
│   └── PersistentVolume (pv-mysql-0)
├── Pod (mysql-1)
│   └── PersistentVolume (pv-mysql-1)
└── Pod (mysql-2)
    └── PersistentVolume (pv-mysql-2)    

```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: mysql
  replicas: 3
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:8.0
          volumeMounts:
            - name: data
              mountPath: /var/lib/mysql
  volumeClaimTemplates:
    - metadata:
        name: data
      spec:
        accessModes: [ "ReadWriteOnce" ]
        resources:
          requests:
            storage: 10Gi
```



#### **DaemonSet Controller**

**Purpose**: Ensures **one Pod runs on every node** (or a subset of nodes).  
**Key Use Case**: Node-level services (e.g., logging agents, monitoring tools).

##### How It Works:

- Automatically adds/removes Pods when nodes join/leave the cluster.

Cluster Nodes
├── Node 1
│   └── Pod (fluentd-logger)
├── Node 2
│   └── Pod (fluentd-logger)
└── Node 3
    └── Pod (fluentd-logger)

```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
spec:
  selector:
    matchLabels:
      name: fluentd
  template:
    metadata:
      labels:
        name: fluentd
    spec:
      containers:
        - name: fluentd
          image: fluentd:latest
```

#### **Job Controller**

**Purpose**: Runs a Pod until **successful completion** (e.g., batch jobs, one-time tasks).  
**Key Use Case**: Data processing, backups, or reports.

##### How It Works:

- Creates Pod(s) and retries until they exit successfully (`exit code 0`).

```
Job (Manages Pods until Completion)
│
├── Pod (batch-job-abcx) → Succeeds
└── Pod (batch-job-defy) → Fails (retries until success)
```

```
apiVersion: batch/v1
kind: Job
metadata:
  name: data-export
spec:
  template:
    spec:
      containers:
        - name: exporter
          image: data-exporter:latest
      restartPolicy: OnFailure
```


####  **CronJob Controller**

**Purpose**: Runs **Jobs on a schedule** (e.g., daily backups).  
**Key Use Case**: Periodic tasks.

##### How It Works:

- Triggers Jobs based on cron-like schedules (e.g., `*/5 * * * *`).

```
CronJob (Schedule-Based Trigger)
│
└── Job (backup-20231001) → Pod (backup-pod-xyz)
└── Job (backup-20231002) → Pod (backup-pod-abc)
```

```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: daily-backup
spec:
  schedule: "0 0 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: backup
              image: backup-tool:latest
          restartPolicy: OnFailure
```

