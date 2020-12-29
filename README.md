
## Project Details:
This project creates a web app that user can register at and login, and upload images to S3 bucket, then show images.

## Steps:
project has docker-compose file to run docker containers, each docker container has pne service whcih are : frontend service, rest API user service, and rest API feed service. both user and feed use the same port and reverseproxy control the incoming traffic between them.

Also, the project has kubernete which run each docker dontainer inside pod in cluster.


1- run docker compose 

docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml build --parallel 

2- Deploy pods

cd ~/cloud/udagram-microservice/udacity-c3-deployment/k8s/
kubectl apply -f backend-user-deployment.yaml
kubectl apply -f backend-user-service.yaml
kubectl apply -f backend-feed-deployment.yaml
kubectl apply -f backend-feed-service.yaml
kubectl apply -f reverseproxy-deployment.yaml
kubectl apply -f reverseproxy-service.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml

3- port-forward 

kubectl port-forward service/frontend 8100:8100
kubectl port-forward service/reverseproxy 8080:8080

