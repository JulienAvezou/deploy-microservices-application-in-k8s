# deploy-microservices-application-in-k8s
Project: Deploy microservices application in k8s with best practices

## 0. Preparation
- Map out what microservices are to be deployed
- Identify and 3rd Pary Services or databases
- Idenitfy which Service is accessible from outside the cluster
- Understand how applications are connected to each other
- What are the image names for each microservice
- What are the env variables for each service
- On which port will microservices be accessible
- In which namespace will applications be deployed

## 1. Create Deployment config & Service config for each Microservice

### 1.1 Create config for first Microservice, the Emailservice (names, labels, ports, image, env vars for connections)

### 1.2 Repeat this step for all other Microservices

### 1.3 Attach volume to redis, emptyDir volume type which exists as long as the pod exists

### 1.4 For Frontend Microservice, deploy a service of type NodePort which makes it accessible externally

## 2. Deploy Microservices in k8s

### 2.1 Create cluster on Linode

### 2.2 Download kubeconfig file, change permissions of file to read-only

### 2.3 Connect to cluster using kubeconfig file

### 2.4 Create namespace and deploy application within that namespace

### 2.5 Access application from the browser to test the deployment

## 3. Improve config.yaml using best practices

### 3.1 Specify image version tags

### 3.2 Configure Liveness Probe on each container to check if app is healthy

### 3.3 Configure Readiness Probe on each container to check if app has started

### 3.4 Configure resource requests for each container

### 3.5 Configure resource limits for each container

### 3.6 Use LoadBalancer type instead of NodePort to create single entrypoint to cluster (or can use Ingress as alternative)

### 3.7 Use more than 1 replica per pod

## 4. Extra best practices

- use more than 1 worker node per cluster
- use labels for all resources
- use namespaces for deployments
- ensure that all images are free of vulnerabilities
- no root access for containers
- update k8s to latest version








