# ReplicaSet

**ReplicaSet** makes your application always available, even if a **Pod** fails. It allows you to have several "replicas" of the application (**Pods**) running at the same time. This is very important to deal with high traffic on the application or ensure that it is always available. In the other words, **ReplicaSet** can manages one or more Pods.

![ReplicaSet](diagrams/ReplicaSet.png)

We can see in the Kubernetes manifest below how to declare a **ReplicaSet**:

```yml
apiVersion: app/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  # Three nginx application replicas
  replicas: 3 
  selector:
    # Ensure that ReplicaSet manages Pods with the same label
    matchLabels:
      app: nginx-app
  # Defines the Pod model that will be replicated
  template: 
    metadata:
      name: nginx-app
      labels:
        app: nginx-app
    spec:
      containers: 
        - name: nginx-container
          image: nginx:stable
          ports:
            - containerPort: 80
```


# Deployments

Esta a uma camada acima do ReplicaSet
Quando criamos um Deployment automaticamente estamos criando um ReplicaSet
Deployment auxiliam com o controle de versionamento e criam um ReplicaSet automaticamente