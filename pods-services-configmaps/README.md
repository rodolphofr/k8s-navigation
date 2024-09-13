# Pods ⚛️

Aspects and true about Pod:

- It is the smallest unit in **Kubernetes**.
- **Pods** are made up of one or more containers.
- With `kubectl` we always create a **Pod**, not a container.
- A *Pod* is considered terminated when all of its containers stop working. If only one container is running, the Pod is considered healthy.

In the following representation we can see that the **Pod** has its own IP address and the containers within it share the same IP address. This allows the containers within the same **Pod** to communicate directly via localhost, facilitating communication between them.

![Pods and containers communication](Pods-And-Containers-Communcation.png)

**Pods** are ephemeral which is why Kubernetes can create and destroy them at any time. If a **Pod** fails, Kubernetes can create another one and replace it, but not necessarily with the same IP address.

## Pods Cheatsheets 👨🏽‍💻

The following commands are being executed imperatively.

```bash
# create a Pod with a container using the ngnix image
kubectl run $pod_name --image=$image_name:$image_version

# show Pods from cluster
kubectl get pods

# show Pods from cluster following the events in real time state
kubectl get pods --watch

# describe a Pod
kubectl describe pods $pod_name 

# deletes a Pod
kubectl delete pods $pod_name

# edit the properties and configurations from Pod
kubectl edit pods $pod_name
```

## Where are images downloaded to Pod containers stored?

When we decide that a new **Pod** will be executed, the **Scheduler** (**sched**) decides in which **Node** this will happen. Then the images downloaded from the Docker Hub will be stored locally on each **Node**, and will not be shared, by default, between all cluster. 

## How create Pod declaratively?

We need a `.yaml` file with the following specifications:

```yaml
# nginx-pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx-container
      image: nginx:stable
```
By executing the `kubectl apply -f nginx-pod.yaml` command, a **Pod** must be created on the cluster **Node**.

To destroy the pod declaratively, you can run `kubectl delete -f nginx-pod.yaml` command.