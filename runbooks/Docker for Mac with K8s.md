# Docker for Mac with Kubernetes
This file describes the default step by step runbook to do a demo with Docker for Mac and Kubernetes.

## Version 
This runbook was tested with Docker for Mac Community Edition Edge Release Version 17.12.0-ce-mac45 - 21669 (last checked 9th of January 2017).

## Preparation steps

To be able to do this demo you need to do the following configuration steps with your Docker for Mac Installation:

* Installation of Kubernetes by using Preferences > Kubernetes > Enable Kubernetes
* Make sure that the system containers are not shown by disable at Preferences > Kubernetes > Show system containers (advanced)

## Before doing the demo

Before you plan to do the demo make sure the following is configured correctly:

* Make sure Docker is running in the mac menu bar
* Make sure Kubernetes is running in the mac menu bar
* Make sure you got the latest version of the DockerCon EU demo application from this repo at k8s > Docker4Mac.
* Make sure that kubectl is configured with the Docker for Mac Kubernetes (if you have multiple Version of Kubernetes installed locally for example Minikube)
 * Check the current kubectl configuration with  ```kubectl config get-contexts```
 * If not correct configure it to use docker-for-mac
 ```kubectl config use-context docker-for-desktop```

## Runbook

1. Show the GUI

* Show the Logo inside the Mac menu bar:
  * Show that Docker is running
  * Show that Kubernetes is running
* Show the About Docker menu and all the componentes installed.
* Show how easy it is to enable Kubernetes with Docker for Mac at Preferences > Kubernetes.

2. Describe the benefits

* Docker for Mac is a single container platform with Kube cluster built-in
* You can now choose between Docker swarm mode and kubernetes
* Full single-node kubernetes cluster using the latest version of docker as the container runtime.
* You can use the concepts of stacks with kubernetes
* You can use Docker compose files or kubernetes manifests

3. Show the current environment from CLI

* Show that you are using the latest client and latest docker engine locally ```docker version```
* Show the current container up and running ```docker container ls```
* Show that there is no pod up and running with kubectl ```kubectl get pods```

4. Show and explain the Demo app from DockerCon EU 2017

* Explain that there are two ways now to deploy the app
  * First is by using a Stack with the docker-compose.yml file
  * Second option is using a Kubernetes manifests file kube-deployment.yaml.

5. Start with the Docker Stack deployment on Kubernetes

* Show the simple docker-compose.yml
* There is a database service db
* There is an API words
* There is a Web frontend
* The compose file has the build settings, and all of the source code is in this directory
* Show the database Dockerfile at db > Dockerfile
 * It is using Postrgres
 * It packages a sql script (words.sql) to deploy the database.
* Show the web frontend Dockerfile at web > Dockerfile
 * The web frontend is a Go application
 * It is using a multi stage Dockerfile
 * The build stage compiles the app at #BUILD
 * And the application stage packages that binary into a tiny image based on alpine at #RUN
* Show the words api Dockerfile at words > Dockerfile
 * It is a Java application
 * It is also using a multi stage Dockerfile
 * It is using openjdk as a base image for the builder at #BUILD
 * And using alpine for the final application image with the JRE and the compiled JAR file.
* Using docker-compose to build the whole application ```docker-compose build```
* Explain if you are using the cache during the build.
* Show what is the current configured orchestrator is Kubernetes with ```docker version```
* Deploy the compose file to Kubernetes with a stack name words1 ```docker stack deploy -c docker-compose.yml words1```
* The app is now running as a Docker stack. You can show and check via ```docker stack ls```
* Show the Docker Services and explain that these are not Swarm services by using the command ```docker stack services words1```
* The Docker Service command shows nothing ```docker service ls```
* Show the Kubernetes Services by using ```kubectl get svc```
* Show the Kubernetes Pods and that the words api has 5 instances by using ```kubectl get pods```
* Each Pod is running a single container
* Show the container by using ```docker container ls```
* Show that the application is running by open a browser on localhost:8080
* The app shows words fetches from the API which served them from the database.
* Explain that this is great because now you can use the latest features of Docker Engine with Kubernetes like the multi stage build. Most of the current solutions out there using old versions of Docker engine.
* remove the current stack by using ```docker stack rm words1```

6. Show the Deployment from a kubernetes manifest

* Show the kube-deployment.yaml 
* It describes the same application in Kubernetes format.
* There is a service and deployment for the database
* There is a service and deployment for the words api
* There is a service and deployment for the web frontend
* Using the same set of Docker images.
* The service for the web frontend is a load balancer which becomes the public endpoint
* Deploy it by using ```kubectl apply -f kube-deployment.yaml```
* Show the kubernetes services by using ```kubectl get svc```
* Show the kubernetes pods by using ```kubectl get pods```
* Show the kubernetes deployments by using ```kubectl get deployments```
* You will not see the docker stack by using ```docker stack ls```
* But you will see the containers running in the Kubernetes pods by using ```docker container ls```
* Open the application by open a browser on port 80 or just using localhost

7. Show the same app running in Docker swarm

* Docker for Mac also has Docker swarm mode build in. You can run also in swarm mode.
* Change the docker cli to use swarm as orchestrator by exporting the environment variable with ```export DOCKER_ORCHESTRATOR='swarm'```
* Show that the Docker cli is now using swarm as the default orchestrator by using ```docker version```
* Initialize the Docker swarm by using ```docker swarm init```
* Now you got a single node docker swarm
* Deploy the stack with the ```docker stack deploy -c docker-compose.yml words3```
* Show the stack by using ```docker stack ls```
* Show the services by using ```docker service ls```
* Show the containers by using ```docker container ls```
* open a browser at localhost:8080 to check the application.


 




