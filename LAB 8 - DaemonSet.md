
Lab 8: DaemonSet in Kubernetes
=============================================================

# ## Create a file named ds-pod.yaml using content given below
```
vi ds-pod.yaml
 ```
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: demo-ds
  labels:
    app: demo-ds
spec:
  selector:
    matchLabels:
      app: demo-ds
  template:
    metadata:
       labels:
           app: demo-ds
    spec:
      containers:
      - name: ds-ctr
        image: quay.io/fluentd_elasticsearch/fluentd:v2.5.2
```
## Save and exit the editor
## Apply the yaml definition to create a fluent-ds DaemonSet
```
kubectl apply -f ds-pod.yaml
```
## Check the available daemonsets in kubernetes cluster
```
kubectl get ds demo-ds
```
## Verify that pods for fluent are created one for each node using DaemonSet
```
kubectl get pods -o wide
```
## Delete the Daemonset created during the lab
```
kubectl delete -f ds-pod.yaml
```
## Verify the pods to find (all) the fluentd pods being deleted from each of the nodes
```
kubectl get pods
```

