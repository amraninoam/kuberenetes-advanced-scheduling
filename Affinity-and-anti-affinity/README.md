# Affinity and Anti-Affinity

### Setup
```sh
# Create our cluster with 4 nodes
kind create cluster --config cluster.yaml
```
```sh
# kgpn alias returns all pods and their node hosts
alias kgpn='kubectl get pod -o=custom-columns=NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName'
```

### Create redis-cache deployment
```sh
# Schedule the redis-cache deployment with a required pod anty affinity of living next to it's self  
kubectl create -f redis-cache.yaml --save-config
```
```sh
# Check if the pods are running
kubectl get pods
```
```sh
# Check on what nodes the pods are running
kgpn
```

### Create web-server deployment

```sh
# Schedule the web-server deployment with a required pod anty affinity of living next to it's self 
# and required pod affinity of living next to a redis pod
 kubectl create -f web-server.yaml --save-config
```
```sh
# Check if the pods are running
kubectl get pods
```
```sh
# Check why is there a Pending pod
kubectl describe pod <pod_name>
```
```sh
# Check on what nodes the pods are running
kgpn
```

### Change web server deployment to preferred podAntiAffinity
```sh
# Comment the required pod anti affinity
sed -i '25,32 s/^/#/' web-server.yaml
```
```sh
# Uncomment the preferred pod anti affinity
sed -i '35,44 s/#/ /' web-server.yaml
```
```sh
# Apply the changes
kubectl apply -f web-server.yaml
```
```sh
# Check if the pods are running
kubectl get pods
```
```sh
# Check on what nodes the pods are running
kgpn
```

### Clean our doings
```sh
# Clean our doings
kubectl get all
kubectl delete -f web-server.yaml
kubectl delete -f redis-cache.yaml
kubectl get all
```