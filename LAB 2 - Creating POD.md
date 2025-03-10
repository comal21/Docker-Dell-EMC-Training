

LAB-2  Creating POD
=============================================================
---------------------------------------------------------------
# Task 1 - Create a pod using below Commands
---------------------------------------------------------------
 ```
 kubectl run pod-1 --image nginx --port 80 
```
# Check the newly created Pod
```
 kubectl get pod
```
```
 kubectl get pod -o wide
```

# Describe Pod using below command
```
 kubectl describe pod pod-1
```
---------------------------------------------------------------
# Task 2 - Create a pod using below yaml
---------------------------------------------------------------
``` 
vi httpd-pod.yaml
``` 
```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
  labels:
    env: prod 
spec:
  containers:
  - name: httpd-container
    image: httpd
    ports:
       - containerPort: 80
 
 ```
# Apply the pod definition yaml
 ```
kubectl create -f httpd-pod.yaml
 ```
 
# Check the newly created Pod
 ```
kubectl get pods
 ```
```
kubectl get pods -o wide
 ```
# Describe Pod using below command
 ```
kubectl describe pod httpd-pod
```
# Enter into a pod
```
kubectl exec -it <podname> -- /bin/bash
```
# Generate yaml file:
```
kubectl run poddemo --image nginx --port 80 --dry-run=client -o yaml > poddemo.yml
```
# Check logs
```
kubectl logs podname
```


