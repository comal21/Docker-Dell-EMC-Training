## Creating pvc 
```
vi pv-claim.yaml
```
```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: sc-claim
spec:
  storageClassName: gp2
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 8Gi
```
## apply the above yaml 
```
kubectl apply -f pv-claim.yaml
```

## verify the pv and pvc

```
kubectl get pvc
```
```
kubectl get pv
```

# Create deployment

```
vi ng-deploy.yaml
```
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: ng-deploy
  name: ng-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ng-pod
  template:
    metadata:
      labels:
        app: ng-pod
    spec:
      volumes:
      - name: cloud-storage
        persistentVolumeClaim:
          claimName: sc-claim
      containers:
      - image: nginx
        name: nginx-ctr
        ports:
        - containerPort: 80
        volumeMounts:
        - name: cloud-storage
          mountPath: /usr/share/nginx/html
```
## verify deployment

```
kubectl get deploy
```
```
kubectl get pods
```

