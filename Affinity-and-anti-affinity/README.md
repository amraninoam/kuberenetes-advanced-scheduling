# Affinity and Anti-Affinity

## Node Affinty 

### Setup
```sh
# Create our cluster with 4 nodes
kind create cluster --config cluster.yml
```
```sh
# Check the default label kubernetes.io/hostname of the pods
kubectl get nodes --show-labels | grep kubernetes.io/hostname=
```
```sh
# kgpn alias returns all pods and their node hosts
alias kgpn='kubectl get pod -o=custom-columns=NAME:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName'
```

### Requierd node affinity
```sh
# Schedule the pod with a required node affinity of kubernetes.io/hostname=advanced-scheduling-worker2  
kubectl create -f podRequierdNodeAffinity.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Check on what node the pod is running
kgpn
```

### Prefferd node affinity

```sh
# Schedule the pod with a Prefferd node affinity of kubernetes.io/hostname=advanced-scheduling-worker3
kubectl create -f podPrefferdNodeAffinity.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Check on what node the pod is running
kgpn
```

### Clean our doings
```sh
# Clean our doings
kubectl delete -f podRequierdNodeAffinity.yml
kubectl delete -f podPrefferdNodeAffinity.yml
```

### optional - required node Affinity
```sh
# change PodNodeRequierdAffinity.yml line n.14 from worker2 to worker3
# Schedule the pod with a required node affinity of kubernetes.io/hostname=advanced-scheduling-worker3
kubectl create -f PodRequierdNodeAffinity.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Describe the pod
kubectl describe pod node-required-affinity
```
```sh
# Clean our doings
kubectl delete -f podRequierdNodeAffinity.yml
```


## Pod Affnity

### Pod required affinity

```sh
# Schedule the pod with a required pod affinity of security=S1
kubectl create -f podRequiredAffinity.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Describe the pod
kubectl describe pod required-pod-affinity
```
```sh
# Schedule the pod with a lable of security=S1
kubectl create -f podS1Security.yml --save-config
```
```sh
# Check if the pods are running
kubectl get pods 
```
```sh
# Check on what node the pod is running
kgpn
```
### Clean our doings

```sh
### Clean our doings
kubectl delete -f podS1Security.yml
kubectl delete -f podRequiredAffinity.yml
```

### Pod preffered affinity

```sh
# Schedule the pod with a preffered pod affinity of security=S2
kubectl create -f podPrefferedAffinity.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Check on what node the pod is running
kgpn
```

```sh
# Schedule the pod with a lable of security=S1
kubectl create -f podS2Security.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Check on what nodes the pods are running now
kgpn
```
```sh
# Delete the pod with a preffered pod affinity of security=S2
kubectl delete -f podPrefferedAffinity.yml
```
```sh
# Schedule again the pod with a preffered pod affinity of security=S2
kubectl create -f podPrefferedAffinity.yml --save-config
```
```sh
# Check if the pod is running
kubectl get pods
```
```sh
# Check on what nodes the pods are running now
kgpn
```

### Clean our doings

```sh
# Clean our doings
kubectl delete -f podPrefferedAffinity.yml
kubectl delete -f podS2Security.yml
```



## Pod Anty Affinity

```sh
# Schedule the pod with a lable of security=S1
kubectl create -f podS1Security.yml --save-config
```
```sh
# Schedule the pod with a lable of security=S2
kubectl create -f podS2Security.yml --save-config
```
```sh
# Check if the pods are running
kubectl get pods
```
```sh
# Check on what nodes the pods are running
kgpn
```
```sh
# Schedule the pod with a required pod anti affinity of security!=S1 && security!=S2
kubectl create -f podAntiAffinity.yml --save-config
```
```sh
# Check if the pods are running
kubectl get pods
```
```sh
# Describe the anti affinity pod
kubectl describe pod required-anti-affinity
```
```sh
# Delete the pod with a lable of security=S2
kubectl delete -f podS2Security.yml
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
kubectl delete -f podAntiAffinity.yml
kubectl delete -f podS1Security.yml
```
