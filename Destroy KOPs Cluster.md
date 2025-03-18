# Delete KOPs cluster
## CleanUp
```
kubectl delete pods --all -n default
```
```
kubectl delete deployments --all -n default
```
```
kubectl delete sts --all -n default
```
```
kubectl get all
```
Delete any custom namespaces created
```
kubectl delete ns <nameofns>
```
Delete any custom created service
```
kubectl delete svc <svcname>
```
Note: Don't delete the default service: Kubernetes
## Use the following command to verify the clusters you have
```
kops get clusters
```
## use the following command to delete the cluster
```
kops delete cluster --name <"full cluster-name"> --state s3://<"full cluster-name"> --yes
```
## Now From AWS console terminate your JumpServer
