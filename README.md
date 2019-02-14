## Deploying Kubernetes On A Local Machine

#### Machine Configuration Used
* Ubunto 18.04
* 8 Gb RAM
* Intel Core i5 (8th gen)

#### Tools Required
* kubectl
* Minikube
* Docker

#### By Docker Image:
* **Step 1:Creating a local kuberntes cluster by minikube**
```bash
minikube start 
eval $(minikube docker-env) 
```
* **Step 2: Packaging a simple nodejs server into a docker container image**
```bash
docker build -t task-app-image:v1 .
```
* **Step 3: Creating a deployment by using the docker image**
```bash
kubectl create deployment task-app --image=task-app-image:v1
```
* **Step 5: Exposing the pod as a service**
```bash
kubectl expose deployment task-app --type=NodePort --port=8080
```
* **Step 6: Running the nodejs server on the kubernetes cluster**
```bash
minikube service task-app
```
This opens the browser window and displays "Hello World"

---------------------------

#### By Deployment file : 
The image reaining the same.
* **Step 1: Defining deployment.yaml file**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: task-app-deployment
spec:
  selector:
    matchLabels:
      app: task-app
  replicas: 1
  template:
    metadata:
      labels:
        app: task-app
    spec:
      containers:
      - name: task-app
        image: task-app-image:v2
        ports:
        - containerPort: 5000
```
* **Step 2: Creating deployment**
```bash
kubectl create -f deployment.yaml
```

