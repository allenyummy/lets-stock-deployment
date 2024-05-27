# Lets Stock Deployment

Use Google Cloud Platform to serve Lets-Stock application.

## Prerequisite

### Create an Artifact Registry
Step 1: Create an Artifact Registry to store docker images.

Step 2: Configure Docker 
```
$ gcloud auth configure-docker ${LOCATION}-docker.pkg.dev
```

### Create an GKE Autopilot Cluster
Step 1: Create an GKE Autopilot Cluster

Step 2: Connect to GKE Autopilot Cluster via command-line
(Check GKE > Connect > Command-line access)

## Deployment

### Push a microservice to Artifact Registry
```
## docker build + docker push
$ docker build -t ${LOCATION}-docker.pkg.dev/${PROJECT_ID}/${REPOSITORY}/${IMAGE} .
$ docker push ${LOCATION}-docker.pkg.dev/${PROJECT_ID}/${REPOSITORY}/${IMAGE}:latest

## cloud build
gcloud builds submit --tag ${LOCATION}-docker.pkg.dev/${PROJECT_ID}/${REPOSITORY}/${IMAGE} .
```

### Deploy to GKE Cluster
```
$ kubectl apply -f deployment.yaml
$ kubectl get deployments
$ kubectl get pods

$ kubectl apply -f service.yaml
$ kubectl get services

$ kubectl apply -f ingress.yaml
$ kubectl get ingress
```
- https://cloud.google.com/kubernetes-engine/docs/quickstarts/deploy-app-container-image
- https://cloud.google.com/kubernetes-engine/docs/deploy-app-cluster
- https://cloud.google.com/kubernetes-engine/docs/tutorials/configuring-domain-name-static-ip
- https://cloud.google.com/kubernetes-engine/docs/how-to/managed-certs