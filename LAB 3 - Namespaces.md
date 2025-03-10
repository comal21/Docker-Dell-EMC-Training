# View namespaces
```
kubectl get ns
```
# Create new ns
```
kubectl create ns dev
```
```
kubectl run pod1 --image nginx -n dev
```
```
kubectl get pods -A
```
```
kubectl get pods -n dev
```
```
kubectl delete ns dev
```
```
kubectl get ns
```
