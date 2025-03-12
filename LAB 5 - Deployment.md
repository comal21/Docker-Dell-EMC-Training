Lab 5 : Deployment
=============================================================

----------------------------------------------------------------------
# Task 1: Write a Deployment yaml and Apply it
----------------------------------------------------------------------
## Create a file named dep-nginx.yaml using content given below
```
vi dep-nginx.yaml
```
## Paste the following content into the file:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-dep
  labels:
    app: nginx-dep
spec:
  replicas: 3
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx-ctr
        image: nginx:1.12.2
        ports:
        - containerPort: 80

```
## Save and exit the editor
## Apply the Deployment yaml created in the previous step
```
kubectl apply -f dep-nginx.yaml
```
## View the objects created by Kubernetes Deployment and ReplicaSet 
```
kubectl get deployments
```
```
kubectl get rs
```
## Access one of the Pods and view nginx version
```
kubectl get pods
```
Pick any one pod part of the deployment and describe it to view its container-image version
```
kubectl describe pod <podname> 
```
Expected output: nginx:1.12.2
-------------------------------------------------------------------------
 # Task 2: Update the Deployment with a Newer Image
-------------------------------------------------------------------------

## Update the nginx image in Pod using below
```
kubectl set image deployment/nginx-dep nginx-ctr=nginx:1.11 --record
```

## Describe the deployment and see that the old pods are replaced with newer ones
```
kubectl describe deployments
```
## Access one of the Pods and view nginx version
```
kubectl get pods
```
Pick any one pod part of the deployment and describe it to view its container-image version
```
kubectl describe pod <podname> 
```
Expected output: nginx:1.11
-----------------------------------------------------------------------------
# Task 3: Rollback of Deployment 
-----------------------------------------------------------------------------

## View the history of Deployments
```
kubectl rollout history deployment/nginx-dep
```
## Rollback the Deployment done in the previous task
```
kubectl rollout undo deployment/nginx-dep --to-revision=1
```
## Access one of the Pods and view nginx version
```
kubectl get pods
```
Pick any one pod part of the deployment and describe it to view its container-image version
```
kubectl describe pod <podname> 
```
Expected output: nginx:1.12.2
------------------------------------------------------------------------------
# Task 4: Scaling of Deployments
------------------------------------------------------------------------------
## View the number of Pod replicas created by the Deployment
```
kubectl get deployments
```
```
kubectl get pods
```
## Scale up the deployment to have 8 Pod replicas
```
kubectl scale deployment nginx-dep --replicas=8
```
## Check the Pods and deployment to and verify that the number of Pod replicas are 8
```
kubectl get deployments
```
```
kubectl get pods
```
## Scale down the deployments to 2 Pod replicas
```
kubectl scale deployment nginx-dep --replicas=2
```
## Check the Pods and deployment to and verify that the number of Pod replicas are down to 2
```
kubectl get deployments
```
```
kubectl get pods
```

-----------------------------------------------------------------------------
# Task 5: Deployment Auto Scaling HPA – Horizontal Pod 
Autoscaling
-----------------------------------------------------------------------------
## Create an HPA (Horizontal Pod Autoscaler):
```
kubectl autoscale deployment nginx-dep --min=3 --max=8 --cpu-percent=70
```
## View the HPA status:
```
kubectl get hpa
```
Expeccted output: The HPA will not work since it depends on another external component : Metric server which has not been setup
-----------------------------------------------------------------------------
# Task 6 Cleanup the resources using below command
-----------------------------------------------------------------------------
## Delete the resources created during the lab:
```
kubectl delete -f dep-nginx.yaml
```
