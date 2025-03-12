# Task 1 : Get Node Label and Create Custom Index.html on Node
## List the worker nodes 
```
kubectl get nodes
```
## Set label to one of the worker node 
```
kubectl label nodes <worker-node-name> role=node
```
## View worker nodes and their labels
```
kubectl get nodes --show-labels | grep role=node
```

## SSH to one of the nodes
```
ssh -t ubuntu@<node_public_IP>
```
## Switch to root
```
sudo su
```
## Run the following commands on the node
```
mkdir /pvdir
```
```
echo Hello World! > /pvdir/index.html
```
```
exit
```
# Task 2 : Create a Local Persistent Volume

## Create a file named pv-volume.yaml using content given below
```
vi pv-volume.yaml
```
```
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume
spec:
  storageClassName: manual
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/pvdir"
```
## Save and exit the editor
## Apply the pv-volume.yaml created in the previous step
```
kubectl apply -f pv-volume.yaml
```
## Check the created PersistentVolume
```
kubectl get pv
```
```
kubectl describe pv pv-volume
```
# Task 3 : Create a Persistent Volume Claim
## Create a file named pv-claim.yaml using content given below
```
vi pv-claim.yaml
```
```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: pv-claim
spec:
  storageClassName: manual
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
```
## Save and exit the editor
## Apply the pv-claim.yaml created in the previous step
```
kubectl apply -f pv-claim.yaml
```
## Check the created PersistentVolumeClaim
```
kubectl get pvc
```
```
kubectl describe pvc pv-claim
```
# Task 4 : Create nginx Pod with NodeSelector
## Create a file named pv-pod.yaml using content given below
```
vi pv-pod.yaml
```
```
kind: Pod
apiVersion: v1
metadata:
  name: pv-pod
spec:
  volumes:
    - name: pv-storage
      persistentVolumeClaim:
        claimName: pv-claim
  containers:
     - name: pv-container
       image: nginx
       ports:
          - containerPort: 80
            name: "http-server"
       volumeMounts:
          - mountPath: "/usr/share/nginx/html"
            name: pv-storage
  nodeSelector:
    role: node
```
## Save and exit the editor
## Apply the pv-pod.yaml created in the previous step
```
kubectl apply -f pv-pod.yaml
```
## View Pod details and see that it is created on the required node
```
kubectl get pods -o wide
```
## Access shell on a container running in your Pod
```
kubectl exec -it pv-pod -- /bin/bash
```
## Run the following commands in the container to verify PersistentVolume
```
apt-get update
```
```
apt-get install curl -y
```
```
curl localhost
```
```
exit
```







