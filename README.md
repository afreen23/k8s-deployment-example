## Deploting Kubernetes On A Local Machine

#### Machine Configuration Used
* Ubunto 18.04
* 8 Gb RAM
* Intel Core i5 (8th gen)

#### Tools Required
* kubectl
* Minikube
* Docker

#### Steps:
* **Step 1: Creating a local kuberntes cluster by minikube**
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
kubectl expose deployment task-app --type=LoadBalancer --port=8080
```
* **Step 6: Running the nodejs server on the kubernetes cluster**
```bash
minikube service task-app
```
This opens the browser window and displays "Hello World"
