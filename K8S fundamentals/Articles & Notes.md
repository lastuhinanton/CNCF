### **working-with-kubernetes-api** / **iximiuz**

![[Pasted image 20250202161305.png]]

* Kubernetes has designed the Kubernetes API to continuously change and grow.

#### kind
* **_kind_** is the name of an **_object schema_**. **_kind_** refers to a particular data structure, i.e. a certain composition of attributes and properties.

kinds are grouped into three categories:

- _Objects_ (`Pod`, `Service`, etc) - persistent entities in the system.
- _Lists_ - (`PodList`, `APIResourceList`, etc) - collections of resources of one or more kinds.
- _Simple_ - specific actions on objects (`status`, `scale`, etc.) **or** non-persistent auxiliary entities (`ListOptions`, `Policy`, etc).

#### objects
* **_Objects_** are persistent entities in the Kubernetes system that represent an _intent_ (desired state) and the _status_ (actual state) of the cluster.

Objects must have more field defined:
- `kind` - a string that identifies the schema this object should have
- `apiVersion` - a string that identifies the version of the schema the object should have
- `metadata.namespace` - a string with the namespace (defaults to "default")
- `metadata.name` - a string that uniquely identifies this object within the current namespace
- `metadata.uid` - a unique in time and space value used to distinguish between objects with the same name that have been deleted and recreated.

![[Pasted image 20250202181951.png]]

### Virtualization-vs-Containerization
https://www.geeksforgeeks.org/virtualization-vs-containerization/

https://habr.com/ru/companies/domclick/articles/566224/