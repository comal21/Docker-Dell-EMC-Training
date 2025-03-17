# Delete KOPs cluster

## Use the following command to verify the clusters you have
```
kops get clusters
```
## use the following command to delete the cluster
```
kops delete cluster --name <"cluster-name"> --state s3://<"cluster-name"> --yes
```
## Now From AWS console terminate your JumpServer
