# Kubernetes services

Kubernetes services help us connect applications together with other applications or users.

# 1 type

1.1 NodePort

Use Case: Access service from outside the cluster

1.2 ClusterIP

Use Case: Internal communication between Pods

Accessible only within the cluster

No external access

1.3 LoadBalancer

Use Case: Exposes the service externally using a cloud provider’s load balancer

Only works with cloud providers (AWS, GCP, Azure, etc.)

# NodePort.yaml

    apiVersion: v1
    kind: Service
    metadata:
        name: my-nodeport-service
    spec:
        selector:
            app: my-app
        type: NodePort
        ports:
            - protocol: TCP
            port: 80        # Service port
            targetPort: 8080 # Pod's port
            nodePort: 30007  # External access port

# clusterIP.yaml

    apiVersion: v1
    kind: Service
    metadata:
        name: my-clusterip-service
    spec:
        selector:
            app: my-app
        ports:
            - protocol: TCP
            port: 80       # Service port
            targetPort: 8080  # Pod's port
        type: ClusterIP

# loadbalancer.yaml

    apiVersion: v1
    kind: Service
    metadata:
        name: my-loadbalancer-service
    spec:
        selector:
            app: my-app
        type: LoadBalancer
        ports:
            - protocol: TCP
            port: 80        # Service port
            targetPort: 8080 # Pod's port
            nodePort: 30007  # External access port




