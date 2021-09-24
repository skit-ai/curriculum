## Kubernetes, an Introduction

This doc is an attempt to give you a crash course on how you can use Kubernetes.

It will give you just enough knowledge to get started with being a consumer of the platform. We will not be delving 
into the depths of components that make up this platform.

This is as gentle an introduction as can be given.

### What is Kubernetes ?

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that 
facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes 
services, support, and tools are widely available. ([source][1])

### Components

When you deploy Kubernetes, you get a cluster.

![2]

This cluster can be divided into 2 parts:

| Component    | Purpose                                                                                                                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Control Pane | This part of your cluster handles the orchestration and management of your deployed components. They effectively manage all the nodes.                    |
| Nodes        | A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node. |

For the rest of this doc, we'll only be concentrating on the Kubernetes objects you can deploy on nodes so that you can familiarize yourself with the basics here.

### Basic Kubernetes Objects

Here, we'll attempt to go through the most commonly used Kubernetes objects.

Kubernetes runs your workload by placing containers into "Pods" to run on Nodes. A node may be a virtual or physical 
machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods.

![3]

The above image shows you a basic architecture of how an application with 3 replicas is deployed in Kubernetes and all 
the Kubernetes objects associated with it. This application has certain secrets and configurations which are stored by 
leveraging the objects Kubernetes provides for that very purpose.

| Object     | Description                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Node       | A Kubernetes cluster is a set of nodes that run containerised applications. The node itself can be called a unit of hardware assigned to the cluster on which applications run. There may be multiple such units. For AWS, this is an EC2 instance.                                                                                                                                                                       |
| Deployment | Controls the container, pod and replica configuration. Auto-creates a ReplicaSet object and pod objects.                                                                                                                                                                                                                                                                                                                  |
| Pod        | Pods are where docker containers run. Resource config of the deployment object will decide CPU and Memory allocated to each pod. All containers within the pod share these resources.                                                                                                                                                                                                                                     |
| Service    | Enables network access to a set of Pods in Kubernetes. Services select Pods based on their labels. When a network request is made to the service, it selects all Pods in the cluster matching the service's selector, chooses one of them, and forwards the network request to it. Service creation automatically creates an endpoint object locally to maintain the IP address mapping of the pods with the K8s cluster. |
| Secret     | Objects which are simple key/value stores where you can keep sensitive data. Values are stored in base64 format. You can use the key from any secret object to inject the secret value into your pod.                                                                                                                                                                                                                     |
| Configmap  | Like secrets, these too are key/value stores where you can keep configurations. Values are stored in plain text.                                                                                                                                                                                                                                                                                                          |

#### A closer look at the Service object

The service object is slightly different from all the other objects listed above. It is used to access the pods within 
the Kubernetes cluster and if required, outside of it as well.

![4]

Difference between a service and a deployment:
* The deployment is tasked with keeping the desired number of pods running.
* The service enables network access to a set of pods.

The number of pods can be scaled up and scaled down by making appropriate changes to the deployment. The pod names or 
IPs themselves can be used to access them individually. However, since they're ephemeral in nature, pods are always 
spawned with new names as well as possibly new IP addresses. 

Hence, the service object is an abstraction that maps to a set of pods to solve this problem. The mapping may span a 
single deployment or multiple deployment objects based on how the service itself is configured.

A request to the service object is then routed to the pods it's mapped to.

### Resources Used

* [Kubernetes Documentation][6]
* [Service - Kubernetes Guide with Examples][5]

[1]: https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/
[2]: resources/components-of-kubernetes.svg
[3]: resources/k8s_basic_arch.jpeg
[4]: resources/service-route.gif
[5]: https://matthewpalmer.net/kubernetes-app-developer/articles/service-kubernetes-example-tutorial.html
[6]: https://kubernetes.io/docs/home/
