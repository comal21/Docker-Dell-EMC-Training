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

## Use the following command to verify the clusters you have
```
kops get clusters
```
## use the following command to delete the cluster
```
kops delete cluster --name <"cluster-name"> --state s3://<"cluster-name"> --yes
```
## Now From AWS console terminate your JumpServer
