Lab 4 : Services in Kubernetes
=============================================================
---------------------------------------------------------------
# Task 1 - Create a file named "svc-pod.yaml" and add the following YAML for a Pod.
---------------------------------------------------------------
```
vi svc-pod.yaml
```
```
apiVersion: v1
kind: Pod
metadata:
  name: svc-pod
  labels:
    app: httpd-ws
spec:
  containers:
  - name: httpd-container
    image: httpd
    ports:
       - containerPort: 80
```

## Apply the Pod definition using the command:
```
kubectl apply -f httpd-pod.yaml
```

## Check the newly created Pod
```
kubectl get pods
```
```
kubectl get pods -o wide
```
## Describe Pod using below command
```
kubectl describe pod httpd-pod
```

----------------------------------------------------------------------
# Task 2  Setup ClusterIP service
----------------------------------------------------------------------

## Create a file named "svc.yaml" and add the following YAML for a ClusterIP Service
```
vi svc.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: test-svc
spec:
  selector:
    app: httpd-ws
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: ClusterIP

```
## Apply above definition using below to create a ClusterIP service
```
kubectl apply -f svc.yaml
```
## Describe the service and verify it has populated the endpoints with IP address matching Pod label
```
kubectl get svc
```
```
kubectl describe svc test-svc
```
## Get EndPoint of the service
```
kubectl get ep  
```

------------------------------------------------------------------------------
# Task 3  Setup NodePort Service
------------------------------------------------------------------------------

## Modify the service created in the previous task to type NodePort
```
vi svc.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: test-svc
spec:
  selector:
    app: httpd-ws
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort
```

## Apply the changes using below command
```
kubectl apply -f svc.yaml
```
## View details of the modified service
```
kubectl describe svc test-svc
```
Note down the NodePort.
## Validate connectivity using External IP on NodePort using below or via browser
```
curl <AnyWorkerNode-Public-IP>:NodePort
```

------------------------------------------------------------------------------------
# Task 4  Setup LoadBalancer Service
------------------------------------------------------------------------------------
## Modify the service created in the previous task to type LoadBalancer 
```
vi svc.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: test-svc
spec:
  selector:
    app: httpd-ws
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```
##  Apply the changes using below command
```
kubectl apply -f svc.yaml
```
## Verify that a new service of type LoadBalancer has been created
```
kubectl get svc
```
```
kubectl describe svc httpd-svc
```
## Access the LoadBalancer on the kops instance or via browser
```
curl <LoadBalancer_DNS>
```


-------------------------------------------------------------------------------
# Task 5 Delete and recreate Pod
-------------------------------------------------------------------------------
## Delete the existing httpd-pod using below
```
kubectl delete -f svc-pod.yaml
```
## View the service details and notice that the Endpoints field is empty
```
kubectl describe svc test-svc
```
## Recreate the httpd Pod and view service details Verify that the endpoints is updated with new Pod IP
```
kubectl apply -f svc-pod.yaml
```
```
kubectl describe svc test-svc
```


--------------------------------------------------------------------------------
# Task 6 Cleanup the resources using below command
----------------------------------------------------------------------------------
## Delete the resources created during the lab:
```
kubectl delete -f svc-pod.yaml
```
```
kubectl delete -f svc.yaml
```
