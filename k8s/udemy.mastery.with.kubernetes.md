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

## Cheetsheet

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

https://cheatography.com/
