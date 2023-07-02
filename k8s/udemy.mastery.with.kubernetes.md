# Udemy Course: Docker Mastery with Kubernetes +Swarm from a Docker Captain
https://www.udemy.com/course/docker-mastery/

Just some notes while I go again through the course. This time only the Kubernetes part.

## Pods

Deploying pods with command line:
```bash
# start a nginx pod
# after run comes ALWAYS the name of the pod 
#    unlike with docker which has random names
kubectl run my-nginx --image nginx

# it returns the pod name and the deployment name
# pod/my-nginx created

# list all pods
kubectl get pods

# remove the pod
kubectl delete pod my-nginx
```

The **pod** is the smallest unit in Kubernetes. It is a group of containers that are deployed together on the same host. It is the smallest unit that can be scheduled to run on Kubernetes. All containers in a pod share the same IP address, IPC, hostname, and other resources. They can also communicate with each other using localhost. They are always co-located and co-scheduled, and run in a shared context on the same node.

When the pod is started the kubernetes uses the **kubelet** which talks to the container runtime (docker) to start the container.
**Every type of resource** which runs containers uses a **pod** under the hood.

## Deployments

**Deployments** are a higher level concept than pods and are used to manage pods. They are used to **deploy and update** applications. They are the recommended way to manage the **creation and scaling** of pods. They are also used to manage the **lifecycle** of pods.

```bash

# create a deployment for nginx
kubectl create deployment nginx --image nginx

```
The **Control Plane** will create a **deployment** then the **controller manager** will create a **replica set** and the replica set will create the **pod**. The **scheduler** will schedule the pod to a node and the kubelet will start the pod. All these resources are stored into the database **(etcd)**.

The pod name structure is constructed from three parts (with example values):
- deployment name: **nginx**
- replica set name: **nginx-7f6d7c87d4**
- pod name: **nginx-7f6d7c87d4-5q8q2**


## Replica Sets

create a simple deployment for apache
```bash
kubectl create deployment my-apache --image httpd
```
scale the deployment to 3 replicas
```bash
kubectl scale deployment my-apache --replicas 3
# or shorter
kubectl scale deploy my-apache --replicas 3
# or 
kubectl scale deploy/my-apache --replicas 3
```

## Custom commands


### for pods

run a ping command in a pod

```bash
# run ping in a pod
kubectl run pingpong --image alpine --command -- ping 8.8.8.8
# get the output 
kubectl logs pingpong
# kill the pod
kubectl delete pod pingpong
```
### for deployments

run a ping command in a deployment

```bash
# run ping in a deployment
kubectl create deployment pingpong --image alpine -- ping 8.8.8.8
# get the output
kubectl logs pingpong
# kill the deployment
kubectl delete deployment pingpong
```


## get command

```bash
# get all pods
kubectl get pods
# get all deployments
kubectl get deployments

# get more information
kubectl get pods -o wide
#or
kubectl get pods --output wide
# or in yaml format
kubectl get pods -o yaml
# ...
```

## describe command

The describe command is used to get more information about a resource (pod, deployment, ...). It will give an overview of the resource and the events that happened to it. Including logs and events.

```bash
# get more information about a pod
kubectl describe pod/my-apache-86c695c9b6-df8bf
# get more information about a deployment
kubectl describe deploy/my-apache
```

## example of inspecting a node

```bash
# get the nodes
kubectl get nodes
# get information about a single node with get first
kubectl get node docker-desktop -o wide
# get more information about the node
kubectl describe node docker-desktop
```

## the watch option

```bash
# watch the pods
kubectl get pods --watch
# watch the nodes
kubectl get nodes --watch
```
example of watching the pods:

```bash
# watch the pods
kubectl get pods --watch

# in another terminal you can also watch the events
kubectl get events --watch
# or to see only the events related to the pods
kubectl get events --watch-only

# in another terminal
kubectl delete pod/my-apache-86c695c9b6-df8bf
# the watch will show the pod being deleted
```

## log command

The log command is used to get the logs of a pod or of multiple pods. It can also be used to follow the logs of a pod.  The logs of a pod are stored in the node where the pod is running. The logs are stored in a file in the node. The log command will get the logs from the file.

```bash
# get the logs of a pod
kubectl logs my-apache-86c695c9b6-df8bf
# get the logs of a deployment
kubectl logs deploy/my-apache
```
In case of deployments by default only the logs of the **first pod** will be shown. And from the first pod will the logs of the **first container** be shown.

**Tail** and **follow** options:

```bash
kubectl logs deploy/my-apache --tail 1 --follow
```

The **tail** option will show the last 1 line of the logs. The **follow** option will follow the logs. It will show the logs as they are written to the file. It will show the logs in real time.

Get the logs from a specific pod and container:

```bash
# to get the container names use the describe command
kubectl describe pod/my-apache-86c695c9b6-df8bf -o yaml
# get the logs from a specific container
kubectl logs pod/my-apache-86c695c9b6-df8bf -c httpd
```

To get all the logs from a pod with multiple containers:

```bash
kubectl logs pod/my-apache-86c695c9b6-df8bf --all-containers=true
```

The `--all-containers` option will get the logs from all the containers in the pod and merge them together.

Get the logs from multiple pods using a label:

```bash
# get the logs from all the pods with the label app=my-apache
kubectl logs -l app=my-apache
```
They are listed one after the other and not interleaved.

## stern

for a better logging experience use stern

```bash
# install stern on a linux machine
# get it from github github.com/stern/stern
stern my-apache
```


## Services 

In k8s a service is an endpoint is consistent so an outside entity can access it So if you want to connect to pods you need a service. The CoreDNS which is a core feature of the **control plane** will resolve the **service** by name. To get traffic to the (pods) service is the job on one of four services:
 - ClusterIP
 - NodePort
 - LoadBalancer
 - ExternalName
 
 ### ClusterIP (default)

Is available **only inside the cluster**. One kubernetes set of pods are talking with another kubernetes set of pods. It gets a single internal virtual IP address selected. It allows other pods in the cluster to reach your **service** and talk to them using the **port** of the service.

Example: *If you create an pod running nginx on port 80 you can create a service that will allow other pods to reach the nginx pod on port 80. The service will have an IP address and a port. The IP address is the IP address of the service and the port is the port of the service. The service will forward the traffic to the nginx pod on port 80.*

### NodePort

Is available **outside the cluster**. It exposes the service on each node's **IP** at a static **port**. It allows **external entities to reach the service** on the node's IP address and the static port. It is useful for development and testing on a single node cluster. It is n**ot recommended for production**.
It will be allocated a high port number between 30000-32767. It will forward the traffic to the service on the port of the service.

### LoadBalancer

Is available **outside the cluster**. It will provision a **load balancer** for the service. It will forward the traffic to the service on the port of the service. It is useful for production. It is not supported on bare metal clusters. It is supported on public clouds like AWS, Azure, GCP, Digital Ocean, ...

Its controling the load balancer of the cloud provider. It will create a load balancer in the cloud provider and forward the traffic to the service on the port of the service.

### ExternalName

Maps the service to the contents of the **externalName** field (e.g. foo.bar.example.com), by returning a **CNAME** record with its value. No proxying of any kind is set up. This requires version 1.7 or higher of kube-dns.
Usually used when need to resolve a name to an external service. It is not used to expose a service. 

### examples of services

create a deployment and scale it to 5 replicas

```bash
# create a deployment
kubectl create deployment httpenv --image=bretfisher/httpenv
# scale up to five replicas
kubectl scale deployment httpenv --replicas=5
```

Create a service of default type ClusterIP and expose it on port 8888. This will create a service with a virtual IP address and a port. The service will forward the traffic to the pods on port 8888. 
With the command `kubectl get svc` you can see the IP address of the service and the port of the service. The IP address is the IP address of the service and the port is the port of the service. The service will forward the traffic to the pods on port 8888.

#### service with ClusterIP

```bash
# create the service of type ClusterIP
kubectl expose deployment/httpenv --port 8888
```

try tp access the service from another pod because cannot be accessed from the host since its a ClusterIP service

```bash
# create a pod with alpine
kubectl run tmp-shell --rm -it --image bretfisher/netshoot -- bash
```

#### service with NodePort

```bash
# create the service of type NodePort
kubectl expose deployment/httpenv --port 8888 --name httpenv-np --type NodePort
```
now you can try the service from the host. this works with DockerDesktop on Windows. It will not work on a cloud provider because it will not have a public IP address.

```bash
# access the service from the host
curl localhost:31001
```
### service with LoadBalancer

This can be done with a cloud provider. It will create a load balancer in the cloud provider and forward the traffic to the service on the port of the service.

DockerDesktop on Windows has a build in load balancer. 

```bash
# create the service of type LoadBalancer
kubectl expose deployment/httpenv --port 8888 --name httpenv-lb --type LoadBalancer

# test the service
curl localhost:8888
```

##  Dry Run and Output YAML

### Deployments

```bash
# create a deployment
kubectl create deployment my-nginx --image nginx --dry-run -o yaml
```
will output something like:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: my-nginx
  name: my-nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: my-nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

### Jobs

Create a dry run job with output yaml

```bash
# create a job
kubectl create job hello --image=busybox --dry-run=client -o yaml -- echo "hello world"
```

the output would be something like:

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: hello
spec:
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - command:
        - echo
        - hello world
        image: busybox
        name: hello
        resources: {}
      restartPolicy: Never
status: {}
```


## Cheetsheet

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

https://cheatography.com/
