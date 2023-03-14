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

![Capture d’écran 2023-03-14 à 18 53 53](https://user-images.githubusercontent.com/62488871/225121951-d4ceea80-2a7d-4fde-a8f9-98a4e863bb0d.png)

### 1.2 Repeat this step for all other Microservices

![Capture d’écran 2023-03-14 à 19 10 21](https://user-images.githubusercontent.com/62488871/225122285-6ae0e410-67ff-41cc-be95-2fb7c91ff315.png)

### 1.3 Attach volume to redis, emptyDir volume type which exists as long as the pod exists

![Capture d’écran 2023-03-14 à 19 05 00](https://user-images.githubusercontent.com/62488871/225122322-76e403a6-f6af-4dd9-ad0e-9d2a01139bda.png)

### 1.4 For Frontend Microservice, deploy a service of type NodePort which makes it accessible externally

![Capture d’écran 2023-03-14 à 19 11 47](https://user-images.githubusercontent.com/62488871/225122371-e2575a60-48ca-47e2-99df-7bdc9330c28b.png)

## 2. Deploy Microservices in k8s

### 2.1 Create cluster on Linode

![Capture d’écran 2023-03-14 à 19 17 29](https://user-images.githubusercontent.com/62488871/225122435-14e5129b-dc82-418f-844d-37278804b61f.png)

### 2.2 Download kubeconfig file, change permissions of file to read-only

![Capture d’écran 2023-03-14 à 19 20 47](https://user-images.githubusercontent.com/62488871/225122525-9c74d608-dc83-4163-88d7-9403a9cbed2a.png)

### 2.3 Connect to cluster using kubeconfig file

![Capture d’écran 2023-03-14 à 19 23 38](https://user-images.githubusercontent.com/62488871/225122560-e626a398-506e-4a92-bf39-491bbd25661c.png)

### 2.4 Create namespace and deploy application within that namespace

![Capture d’écran 2023-03-14 à 19 25 43](https://user-images.githubusercontent.com/62488871/225122588-fa16322b-c3c1-4135-8c4c-86408cb34e6f.png)

![Capture d’écran 2023-03-14 à 19 27 43](https://user-images.githubusercontent.com/62488871/225122632-331f2b36-d71a-4a01-80ff-2a711961efd2.png)

### 2.5 Access application from the browser to test the deployment

![Capture d’écran 2023-03-14 à 19 29 11](https://user-images.githubusercontent.com/62488871/225122737-e7f5a73e-50c8-43e7-ab2a-7894cf2bd230.png)

<img width="1435" alt="Capture d’écran 2023-03-14 à 19 31 41" src="https://user-images.githubusercontent.com/62488871/225122753-59942e48-9649-47b2-91c5-2cb420f2d73a.png">

## 3. Improve config.yaml using best practices

### 3.1 Specify image version tags

![Capture d’écran 2023-03-14 à 19 34 04](https://user-images.githubusercontent.com/62488871/225122806-b00bb162-99df-4b4c-8acb-3f1b86461668.png)

### 3.2 Configure Liveness Probe on each container to check if app is healthy

![Capture d’écran 2023-03-14 à 19 59 43](https://user-images.githubusercontent.com/62488871/225122857-1f010e49-221f-469e-88d8-8ab8139ba5ae.png)

### 3.3 Configure Readiness Probe on each container to check if app has started

![Capture d’écran 2023-03-14 à 19 59 48](https://user-images.githubusercontent.com/62488871/225122920-e29e5b9d-4989-4847-8560-fff8e5de9441.png)

### 3.4 Configure resource requests & limits for each container

![Capture d’écran 2023-03-14 à 20 16 19](https://user-images.githubusercontent.com/62488871/225122980-f76c52c8-cae0-47a6-9702-7c1cf787b579.png)

### 3.5 Use LoadBalancer type instead of NodePort to create single entrypoint to cluster (or can use Ingress as alternative)

![Capture d’écran 2023-03-14 à 20 29 01](https://user-images.githubusercontent.com/62488871/225123148-c39bfd89-56a4-49ca-9ace-f440570040f4.png)

### 3.6 Use more than 1 replica per pod

![Capture d’écran 2023-03-14 à 20 35 53](https://user-images.githubusercontent.com/62488871/225123225-92783a66-8a99-429b-af26-7d5bdfcb1de4.png)

## 4. Extra best practices

- use more than 1 worker node per cluster
- use labels for all resources
- use namespaces for deployments
- ensure that all images are free of vulnerabilities
- no root access for containers
- update k8s to latest version
