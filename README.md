# k8s-cvdupdate
A Kubernetes solution for utilizing cvdupdate.

This is just a simple set of YAMLs to facilitate running your own private mirror for 
ClamAV updates. This makes use of [docker-cvdupdate](https://hub.docker.com/r/tilleyc/cvdupdate), which is a
image that will run [cvdupdate](https://github.com/Cisco-Talos/cvdupdate) and automatically process
the downloads in an approved manner. It stores these definition downloads on a shared volume
with an nginx container, which can serve them to your clients.

## How-to

 - Create a namespace for the application with `kubectl create namespace <namespace>`
 - Apply either the deployment file (2 replicas), or the standalone (single instance), depending on what you want.
   `kubectl apply -f cvdupdate-deployment.yaml`
 - Apply the service config to expose the web server so you can then pull images.
   `kubectl apply -f cvdupdate-service.yaml`
  - Get your service IP with `kubectl get service`, and point your clients to it.

## @TODO

 - Create Helm chart to make it even easier to deploy.
