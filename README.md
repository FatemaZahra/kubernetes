# Kubernetes

Kubernetes (also known as k8s or “kube”) is an open source container orchestration platform that automates many of the manual processes involved in deploying, managing, and scaling containerized applications.

# Benefits of kubernetes

- Reduced application development and release timeframes
- Optimization of IT costs
- Increased software scalability and availability
- Flexibility in multi-cloud environments
- Cloud portability.

## Kubernetes Installation

- From the Docker Dashboard, select the Setting icon.
- Select Kubernetes from the left sidebar.
- Next to Enable Kubernetes, select the checkbox.
- Select Apply & Restart to save the settings and then click Install to confirm.
- Use Command on CLI: `kubectl get svc` to check if Kubernetes is installed

## Creating Clusters

```t
# K8 works with API versions to declare the resources
# We have to declare the API version and the kind of service/component
# Services: Deployment, service, pods, replicasets, crobjob, autoscaling group

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment # naming the deployment
spec:
  selector:
    matchLabels:
      app: nginx # look for this label to match with k8 service

  # Let's create a replica set of this with 3 instances/pods
  replicas:
    3
    # template to use it's label for k8 service to launch in the browser
  template:
    metadata:
      labels:
        app: nginx # this label connects to the service or any other k8 components
    # Let's define the container spec
    spec:
      containers:
        - name: nginx
          image: fatemazahra/eng122_nginx_web_hosting:latest
          ports:
            - containerPort: 80
# create a kubernetes nginx-service.yml to create a k8 service

```

- To Create: `kubectl create -f nginx-deploy.yml`
- Get Deployed: `kubectl get deploy`
- Get Pods: `kubectl get pods`
- Delete pods: `kubectl delete pod nginx-deployment-f45fcb4f6-8fg22`
- Delete deployment: `kubectl delete deplo name-of-deployment`

## Create a service

```t
# Select the type of API version and type of service/object

apiVersion: v1

kind: Service

# Metadata for name

metadata:
  name: nginx-svc

  namespace: default # sre

# Specificaition to include ports Selector to connecto to the deployment

spec:
  ports:
    - nodePort: 30442 # range is 30000-32768

      port: 80

      protocol: TCP

      targetPort: 80

  # Let's define the selector and label to connect to nginx deployment

  selector:
    app: nginx # this label connects this service to deployment

  # Creating NodePort type of deployment

  type: NodePort # also use LoadBalancer -  for local use cluster IP

```

To create: `kubectl create -f nginx-service.yml`
To edit: `kubectl edit deploy nginx-deployment`

```

```
