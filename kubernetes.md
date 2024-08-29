# Kubernetes:
  * Kubernetes is an open source container orchestration engine for automating deployment, scaling, and management of containerized applications.
  * Kubernetes provides with:
     a) Service discovery and load balancing
     b) Storage orchestration
     c) Automated rollouts and rollbacks
     d) Self-healing
     e) Secret and configuration management
     f) Horizontal scaling
  * K8s is cluster so we interact with master nodes. There are two ways of interacting, where as for k8s. It exposes APIs. From code/restapi with json. From command line where k8s gives a cmd line tools kubectl .  

# Kuberentes Architecture:
K8s at the node level has two types of nodes
* Master nodes
* Node  

kube-apiserver:
   * The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane. This is way to interact with k8s cluster
Etcd:
   * Consistent and highly-available key value store used as Kubernetes backing store for all cluster data.
kube-scheduler:
   * The kube-scheduler is a key component of Kubernetes that is responsible for scheduling pods onto the nodes in a Kubernetes cluster. It determines which node is most suitable for running a given pod based on various factors such as resource requirements, affinity/anti-affinity rules, and other constraints.
kube-controller-manager:
   * The kube-controller-manager is a core component of the Kubernetes control plane responsible for managing various controllers that handle the operational aspects of the cluster. 
   * There are many different types of controllers. Some examples of them are:
     a) Node controller: Responsible for noticing and responding when nodes go down.
     b) Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
     c) EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
     d) ServiceAccount controller: Create default ServiceAccounts for new namespaces.   
Cloud-controller-manager:
   * The cloud-controller-manager is a component in Kubernetes that interacts specifically with cloud provider APIs to manage resources related to cloud infrastructure.

Node components:
kubelet:
  * An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
kube-proxy:
   *  kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.
Container runtime:
   * A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment.
   * Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI (Container Runtime Interface)
# Cri-dockerd(Container Runtime Interface):
* The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components.
* We need a working container runtime on each Node in your cluster, so that the kubelet can launch Pods and their containers.
* The Container Runtime Interface (CRI) is the main protocol for the communication between the kubelet and Container Runtime.
## Compute:
* In cloud computing, the term “compute” describes concepts and objects related to software computation. It is a generic term used to reference processing power, memory, networking, storage, and other resources required for the computational success of any program
# Kubernetes Workloads:
## Pod:
* Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
* A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.
* Each Pod in k8s cluster gets a unique ip address
* In Kubernetes, pods, ReplicaSets, and deployments are referred to as objects(Objects are things you create in your Kubernetes cluster to represent how you want your applications or resources to be set up and run) or workloads.
## Manifest file:
apiVersion: The `apiVersion` field in a Kubernetes YAML file specifies the version of the Kubernetes API that the resource adheres to. It ensures compatibility between the YAML file and the Kubernetes cluster. For instance, `apiVersion: v1` corresponds to the core Kubernetes API. 
kind: The `kind` field defines the type of resource being created or modified.
metadata: The `metadata` field contains essential information about the resource, such as its name, labels, and annotations.
spec: The `spec` field describes the desired state of the resource. It outlines the configuration details and behavior of the resource
status: The `spec` field describes the desired state of the resource. It outlines the configuration details and behavior of the resource
# Pod life cycle:
# Pod phase:
## Pending: 
* The Pod has been accepted by the Kubernetes cluster, but one or more of the containers has not been set up and made ready to run.
## Running:
* The Pod has been bound to a node, and all of the containers have been created. At least one container is still running, or is in the process of starting or restarting.
## Succeeded:
* All containers in the Pod have terminated in success, and will not be restarted.
## Failed:
* All containers in the Pod have terminated, and at least one container has terminated in failure. That is, the container either exited with non-zero status or was terminated by the system, and is not set for automatic restarting.
## Unknown:
* For some reason the state of the Pod could not be obtained. This phase typically occurs due to an error in communicating with the node where the Pod should be running.

# RestartPolicy:
## Always: 
* Automatically restarts the container after any termination.
## OnFailure: 
* Only restarts the container if it exits with an error (non-zero exit status).
## Never: 
* Does not automatically restart the terminated container.

# Containers:
## initContainers:
* List of initialization containers belonging to the pod. Init containers are executed in order prior to containers being started. If any init container fails, the pod is considered to have failed and is handled according to its restartPolicy. The name for an init container or normal container must be unique among all containers. Init containers may not have Lifecycle actions, Readiness probes, Liveness probes, or Startup probes. 
## containers:
* List of containers belonging to the pod. Containers cannot currently be added or removed. There must be at least one container in a Pod. Cannot be updated.
## EphemeralContainers:
* Ephemeral containers may be run in an existing pod to perform user-initiated actions such as debugging.  In order to add an ephemeral container to an existing pod, use the pod's ephemeralcontainers subresource.

## Debugging and troubleshooting:
* While debugging focuses on small, local instances that can be identified and fixed in one session, troubleshooting is a holistic process that takes into account all of the components in a system, even the team’s processes, and the way they affect each other.

# Replication Controller:
* A ReplicationController ensures that a specified number of pod replicas are running at any one time. In other words, a ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available.
* The pods maintained by a ReplicationController are automatically replaced if they fail, are deleted, or are terminated.
* The ReplicationController uses equality-based selectors only.
Eg for equality-based:
* app: nginx
  
# Label and selector:
## Label:
* Labels are key/value pairs that are attached to objects such as Pods.
* Labels can be attached to objects at creation time and subsequently added and modified at any time.
* Each Key must be unique for a given object.
## Selector:
* Selector helps us to filter the items/objects which have labels attached to them.
# Replica Set:
* A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time.
* The ReplicaSet extends the functionality of the ReplicationController by supporting both equality-based and set-based selectors.
Eg for set-based:
* matchExpressions:
    - key: tier
      operator: In
      values:
      - frontend
* Replica Sets changes can be tracked and that is what the deployment uses. 
# Kubernetes Metrics Server:
* Metrics Server is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines.
* Metrics Server collects resource metrics from Kubelets and exposes them in Kubernetes apiserver through Metrics API for use by Horizontal Pod Autoscaler and Vertical Pod Autoscaler. Metrics API can also be accessed by kubectl top, making it easier to debug autoscaling pipelines.
# Service:
* In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster.
* We use a Service to make that set of Pods available on the network so that clients can interact with it.
* For some parts of  application (for example, frontends) you may want to expose a Service onto an external IP address, one that's accessible from outside of your cluster.
## ClusterIP:
* Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service.
## NodePort:
* Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP.
## LoadBalancer:
* Exposes the Service externally using an external load balancer. Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider.
## ExternalName:
* Maps the Service to the contents of the externalName field (for example, to the hostname api.foo.bar.example). The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value.

# Resource Limits:
* When you specify a Pod, you can optionally specify how much of each resource a container needs. The most common resources to specify are CPU and memory (RAM)
* When you specify the resource request for containers in a Pod, the kube-scheduler uses this information to decide which node to place the Pod on. When you specify a resource limit for a container, the kubelet enforces those limits so that the running container is not allowed to use more of that resource than the limit you set.
* If the node where a Pod is running has enough of a resource available, it's possible (and allowed) for a container to use more resource than its request for that resource specifies. However, a container is not allowed to use more than its resource limit.
# Probes in K8s:
## Liveness:
* The kubelet uses liveness probes to know when to restart a container. For example, liveness probes could catch a deadlock, where an application is running, but unable to make progress. Restarting a container in such a state can help to make the application more available despite bugs.
  
## Readiness:
* The kubelet uses readiness probes to know when a container is ready to start accepting traffic. A Pod is considered ready when all of its containers are ready. One use of this signal is to control which Pods are used as backends for Services. When a Pod is not ready, it is removed from Service load balancers.
  
## Startup:
* The kubelet uses startup probes to know when a container application has started. If such a probe is configured, liveness and readiness probes do not start until it succeeds, making sure those probes don't interfere with the application startup.  

# Daemonset:
* A DaemonSet ensures that all (or some) Nodes run a copy of a Pod.
* Deleting a DaemonSet will clean up the Pods it created.
* Some typical uses of a DaemonSet are
    a) Running a cluster storage daemon on every node.
    b) Running a logs collection daemon on every node.
    c) Running a node monitoring daemon on every node.

# Deployment Strategies:
* A Deployment provides declarative updates for Pods and ReplicaSets.
## https://medium.com/@muppedaanvesh/rolling-update-recreate-deployment-strategies-in-kubernetes-%EF%B8%8F-327b59f27202
## Deployment in blue and green:
* Blue-green deployment is a popular deployment strategy in Kubernetes that runs two versions of your app side-by-side, with traffic directed to the old release until you promote the new one. 
* A Blue-Green Deployment is a deployment strategy where two identical environments, the “blue” environment and the “green” environment, are set up. The blue environment is the production environment, where the live version of the application is currently running, and the green environment is the non-production environment, where new versions of the application are deployed.
* When a new version of the application is ready to be deployed, it is deployed to the green environment. Once the new version is deployed and tested, traffic is switched to the green environment, making it the new production environment. The blue environment then becomes the non-production environment, where future versions of the application can be deployed.
## Canary Deployments:
* In a canary deployment, a new version of the application is rolled out gradually. A small percentage of traffic is routed to the new version (the "canary"), while the majority continues to hit the old version.
  
## Recreate Deployment:
* Recreate deployment strategy involves terminating all existing instances of pods before creating new ones. It leads to downtime during the update process but ensures a clean, predictable transition.
## Rolling Update:
* Rolling update is the default deployment strategy in Kubernetes. It ensures that your application is updated gradually, by replacing old instances with new ones in a controlled manner.
* The rollout is managed by controlling parameters like maxUnavailable and maxSurge.
* maxUnavailable: Specifies the maximum number or percentage of pods that can be unavailable during the update. Default is 25%. This means that during the update, at least 75% of the desired number of pods must be available.
* maxSurge: maxSurge is the maximum number of extra Pods that can be added during an update to make sure your application stays available.
Example: If you normally have 10 Pods running, and maxSurge is set to 2, Kubernetes might temporarily run 12 Pods during the update to keep your app running smoothly while it replaces the old Pods with new ones.
# Kubernetes Storage
To persist the data in the Read/Write Layer, docker has volumes.
K8s supports volumes to persist the data. The types of volumes which are supported by k8s are
## Volume:
This gives volume with the help of mnt namespace to the container.
Volume’s lifecyle is equivalent to lifecycle of Pod
## Ephemeral Volume:
This is also temporary volume used for containers where they require anypersistent storage across Pod restarts/creations.
## Persistent Volume:
* This stores volumes and has no relation with life time of Pod.
* This uses Storage Classes which help for dynamic provisioing of storage (i.e.create azure managed disk or ebs volume or azure fileshare or aws elastic filesystem automatically) or admins manually provisioning storage and providingit as storage class.
* A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual Pod that uses the PV

## PersistentVolumeClaim:
* A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany, ReadWriteMany, or ReadWriteOncePod, see AccessModes).
Access Modes:
## ReadWriteOnce:
* The volume can be mounted as read-write by a single node. ReadWriteOnce access mode still can allow multiple pods to access the volume when the pods are running on the same node. 
## ReadOnlyMany:
* The volume can be mounted as read-only by many nodes.
## ReadWriteMany:
* The volume can be mounted as read-write by many nodes.
## ReadWriteOncePod:
* The volume can be mounted as read-write by a single Pod. Use ReadWriteOncePod access mode if you want to ensure that only one pod across the whole cluster can read that PVC or write to it.

# Stateful Sets:
* StatefulSet is the workload API object used to manage stateful applications.
* Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.
* Like a Deployment, a StatefulSet manages a group of Pods that all run the same application. However, unlike a Deployment, each Pod in a StatefulSet has a unique, stable identity (like a name or number) that sticks with it, even if the Pod is restarted or moved to a different node.
* In a Deployment, all Pods are identical and interchangeable. In a StatefulSet, each Pod is unique and keeps its identity, making it ideal for applications that need stable, consistent connections to storage or other resources.
* Deleting and/or scaling a StatefulSet down will not delete the volumes associated with the StatefulSet.
* StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods.
* StatefulSets do not provide any guarantees on the termination of pods when a StatefulSet is deleted. To achieve ordered and graceful termination of the pods in the StatefulSet, it is possible to scale the StatefulSet down to 0 prior to deletion
  
# Headless Service:
* Sometimes you don't need load-balancing and a single Service IP. In this case, you can create what are termed headless Services, by explicitly specifying "None" for the cluster IP address (.spec.clusterIP)
* A headless Service in Kubernetes is a type of Service where you don't need load-balancing or a single Service IP. Instead of routing traffic through a load balancer, each Pod in a headless Service can be accessed directly.
* In a headless Service, you explicitly set the clusterIP to None, meaning no cluster IP is assigned, and no load balancing is done by Kubernetes.
* Instead of using a single IP, the DNS of the headless Service returns the IP addresses of all the individual Pods, so clients can connect directly to any specific Pod.

# Config Maps:
* A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.
  
# Secrets:
*   A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.

# Kubernetes Namespaces:
* In Kubernetes, namespaces provide a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.)
* Namespaces are intended for use in environments with many users spread across multiple teams, or projects. 
## Types:
### default
Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace.
### kube-node-lease
This namespace holds Lease objects associated with each node. Node leases allow the kubelet to send heartbeats so that the control plane can detect node failure.
### kube-public
This namespace is readable by all clients (including those not authenticated). This namespace is mostly reserved for cluster usage, in case that some resources should be visible and readable publicly throughout the whole cluster. The public aspect of this namespace is only a convention, not a requirement.
### kube-system
The namespace for objects created by the Kubernetes system.
# Jobs & Cron Jobs:
## Job:
* A Job in Kubernetes is used to run a one-time task. Once the Job completes its task successfully, it doesn't run again unless manually triggered
## CronJob:
* A CronJob creates Jobs on a repeating schedule.
* CronJob is meant for performing regular scheduled actions such as backups, report generation, and so on. One CronJob object is like one line of a crontab (cron table) file on a Unix system. It runs a Job periodically on a given schedule, written in Cron format.

# Horizontal Pod Autoscaler:
* In Kubernetes, a HorizontalPodAutoscaler automatically updates a workload resource (such as a Deployment or StatefulSet), with the aim of automatically scaling the workload to match demand.
* If the load decreases, and the number of Pods is above the configured minimum, the HorizontalPodAutoscaler instructs the workload resource (the Deployment, StatefulSet, or other similar resource) to scale back down.
* The horizontal pod autoscaling controller, running within the Kubernetes control plane, periodically adjusts the desired scale of its target (for example, a Deployment) to match observed metrics such as average CPU utilization, average memory utilization, or any other custom metric you specify

# Scheduling in K8s using taints and tolerations:
* Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite they allow a node to repel a set of pods.
* Tolerations are applied to pods. Tolerations allow the scheduler to schedule pods with matching taints.
* Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes.
## NoExecute
This affects pods that are already running on the node as follows:
Pods that do not tolerate the taint are evicted immediately
Pods that tolerate the taint without specifying tolerationSeconds in their toleration specification remain bound forever
Pods that tolerate the taint with a specified tolerationSeconds remain bound for the specified amount of time. After that time elapses, the node lifecycle controller evicts the Pods from the node.
## NoSchedule
No new Pods will be scheduled on the tainted node unless they have a matching toleration. Pods currently running on the node are not evicted.
## PreferNoSchedule
PreferNoSchedule is a "preference" or "soft" version of NoSchedule. The control plane will try to avoid placing a Pod that does not tolerate the taint on the node, but it is not guaranteed.

# Annotations:
* we can use Kubernetes annotations to attach arbitrary non-identifying metadata to objects. Clients such as tools and libraries can retrieve this metadata and annotations are key-value pairs that can be added to Kubernetes objects like Pods, Services, Deployments, etc., to store non-identifying metadata. 
* Annotations are primarily used to attach additional information that doesn't directly affect the operation of the Kubernetes object
# Ingress and Ingress Controller
* Ingress in Layer 7 load balancer.
* When we need path based or hostname based routing we can use ingress.
* Ingress supports layer7 lb with in k8s cluster but to expose this functionality outside of k8s clusterit needs ingress controller.
* k8s doesnot have default ingress controller.
* There are many free ingress controller
   1) nginx ingress controller
   2) haproxy ingress controller
   3) contour ingress controller
* All the cloud providers have layer 7 lb they support cloud specific ingress controller
* AWS supports application load balancer ingress controller
* Azure supports application gateway ingress controller.

Kubernetes commands:

* kubectl api-resources # To get all the api-resources in your k8s cluster
* kubectl get nodes # To get list of nodes
* kubectl get no
* kubectl get no -o wide # Extended view of the nodes in your Kubernetes cluster, displaying more detailed information
* kubectl apply -f <manifest.yml>
* kubectl get pods or kubectl get po
* kubectl get pods -o wide
* kubectl describe pods <podname>  
* kubectl get pods hello-pod -o yaml
* kubectl delete -f <manifest.yml>
* kubectl run nginx --image=nginx --restart=Never # Declarative approach 
* kubectl get rc
* kubectl delete pod <podname>
* kubectl scale rs <replicaname> --replicas=2 # Scale a ReplicaSet to a specified number of replicas
* kubectl exec -it <pod-name> -- <shell /bin/bash /bin/sh> # Getting inside containers
* kubectl exec <pod-name> -- <linux command>
* kubectl get svc # To get service
* kubectl get ep # To get endpoints
* kubectl get endpointeslices
* kubectl rollout history deployments/<deplomentname> # Used in Kubernetes to view the revision history of a specific deployment
* kubectl rollout undo deployments/<deplomentname> --to-revision=1
* kubectl rollout status deployments/<deplomentname>
* kubectl get pvc
* kubectl get jobs --namespace <namespacename>  
* kubectl get hpa
* kubectl taint nodes ip-10-0-1-119.us-east-2.compute.internal poc=true:NoSchedule 

# https://kubernetes.io/docs/reference/kubectl/quick-reference/ 
 



