# K8S * yaml

to apply a configuration file to k8s cluster, use `kubectl apply -f <file>`
to delete a configuration file from k8s cluster, use `kubectl delete -f <file>`
to get a configuration file from k8s cluster, use `kubectl get -f <file> -o yaml`

The `apply` command works also on directories, so you can apply all the files in a directory with `kubectl apply -f <dir>`

Also `apply` can take an URL as argument, so you can apply a configuration file from a remote location with `kubectl apply -f <url>`

### yaml vs json

The `kubectl` command can take as argument both `yaml` and `json` files, but `yaml` is the preferred format. `yaml` is more human readable and it supports comments. `json` is more compact and it is the format used by the k8s API.

So you write your configuration files in `yaml` and `kubectl` converts them to `json` before sending them to the k8s API.

Also you can mix and match `yaml` and `json` files in the same directory. 

You can have all the resources in a single file or you can have a file for each resource.

### Resources & Manifests

A full description of a resource is called a **manifest**.
Each Manifest has **four root keys**. The root keys are `apiVersion`, `kind`, `metadata` and `spec`.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
  ports:
    - containerPort: 80
```

example of a manifest for a deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```
add also the service to the deployment. See the three dashes `---` that separate the two manifests.

```yaml 
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
  selector:
    type: front-end
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```
## Kind & API Version

get all types of resources with `kubectl api-resources`

`APIGROUP` is the group of the resource. There you can find the API version of the resource. For example `apps/v1` means that the resource is in the `apps` group and the version is `v1`.

Command to get the API version:

```bash
kubectl api-versions
```

