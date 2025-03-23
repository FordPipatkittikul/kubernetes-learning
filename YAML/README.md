# YAML file

It is used to represented configuration data. Something to keep in mind list is ordered but dictionary is unordered

![alt text](<Screenshot (161).png>)


# YAML in Kubernetes

## 1 Pods

    apiVersion: v1   # Specifies Kubernetes API version
    kind: Pod        # Defines the resource type (Pod)
    metadata:        # Metadata section contains information about the Pod
        name: my-pod   # Name of the pod
        labels:        # Labels are key-value pairs used for selection
            app: my-app
    spec:            # Specification for the Pod
        containers:    # List of containers inside the Pod
        - name: my-container # Name of the container
          image: nginx       # Docker image to be used
          ports:
          - containerPort: 80  # Exposes port 80 inside the container


## 2 ReplicaSet

- Ensures a specified number of pod replicas are running at all times.
- If a pod crashes or is deleted, the ReplicaSet creates a new one.

    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
        name: my-replicaset
    spec:
        replicas: 3  # Ensures three pod replicas are running
        selector:    # Defines how ReplicaSet finds Pods to manage
            matchLabels:
                app: my-app
        template:    # Defines the Pod template for creating new replicas
            metadata:
                name: my-pod
                labels:
                    app: my-app
            spec:
                containers:
                - name: nginx-container
                  image: nginx
                  ports:
                  - containerPort: 80

## 3 Deployments

- Manages ReplicaSets and provides rolling updates and rollbacks.
- Allows declarative updates to applications.
- Ensures zero-downtime updates and self-healing.

    apiVersion: apps/v1
    kind: Deployment
    metadata:
        name: myapp-deployment
    spec:
        replicas: 3  
        selector:    
            matchLabels:
                app: my-app
        template:    
            metadata:
                name: my-pod
                labels:
                    app: my-app
            spec:
                containers:
                - name: nginx-container
                  image: nginx
                  ports:
                  - containerPort: 80