## Interacting with Kubernetes

- We will interact with our Kubernetes cluster through the Kubernetes API
- The Kubernetes API is (mostly) RESTful
- It allows us to create, read, update, delete *resources*
- A few common resource types are:
  - node (a machine — physical or virtual — in our cluster)
  - pod (group of containers running together on a node)
  - service (stable network endpoint to connect to one or multiple containers)

![Node, pod, container](./images/k8s-arch3-thanks-weave.png)

# First contact with `kubectl`

- `kubectl` is (almost) the only tool we'll need to talk to Kubernetes

- It is a rich CLI tool around the Kubernetes API

  (Everything you can do with `kubectl`, you can do directly with the API)

- On our machines, there is a `~/.kube/config` file with:

  - the Kubernetes API address
  - the path to our TLS certificates used to authenticate

- You can also use the `--kubeconfig` flag to pass a config file
- `kubectl` can be pronounced "Cube C T L", "Cube cuttle", "Cube cuddle"...

---

## `kubectl get`

- Let's look at our `Node` resources with `kubectl get`!

```
kubectl get nodes
kubectl get nodes -o wide
kubectl get nodes -o yaml
kubectl get nodes -o json
```
(Ab)using `kubectl` and `jq`

```
kubectl get nodes -o json |
            jq ".items[] | {name:.metadata.name} + .status.capacity"
```

## `kubectl describe`

- `kubectl describe` will retrieve some extra information about the resource

```
kubectl describe node node1
```
