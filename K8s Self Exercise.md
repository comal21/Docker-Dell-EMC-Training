### Problem Statement 1:
##
Create a Kubernetes **Pod** running an **nginx** container. Ensure that the Pod is accessible on port **8080** within the cluster.
   - After the Pod is created, exec into the container and verify that **nginx** is running.
   - The nginx Pod should serve a custom HTML page with the text "Welcome to Kubernetes training."
   - Use Yaml Approach to create the pod.
   - Hint: Default nginx path:/usr/share/nginx/html/index.html
##

### Problem Statement 2:
##
Create a Namespace called web-app.
Create a Deployment for the web application, consisting of a simple nginx container within the web-app ns.
The Deployment should have 3 replicas for high availability, meaning 3 Pods should be running at all times.
Ensure that the nginx container serves content on port 8080.
Create a LoadBalancer Service that exposes the nginx Deployment externally on port 80.
##

### Problem Statement 3:
## 
Create a daemon set for the monitoring tool promethues: prom/prometheus:v2.31.1
in the monitoring namespace
##

