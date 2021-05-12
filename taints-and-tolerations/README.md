# Taints and Tolerations
# Set Aliases
Add these aliases to your session
```sh
# kgpn alias returns all pods and their node hosts
alias kgpn='kubectl get pods -o jsonpath='"'"'{range .items[*]}{@.metadata.name}{" "}{@.spec.nodeName}{"\n"}{end}'"'"''
# kgnot alias returns all nodes and their taints.
alias kgnot='kubectl get nodes -o jsonpath='"'"'{range .items[*]}{@.metadata.name}{" "}{@.spec.taints[*].key}:{@.spec.taints[*].value}-{@.spec.taints[*].effect}{"\n"}{end}'"'"''
```

# NoExecute (hard) Taints example
```sh
# Schedule the pod with tolerations
kubectl create -f taints-and-tolerations/deployment-without-tolerations.yaml --save-config
```

```sh
# Check which node this pod was scheduled on
kgpn
```

```sh
# Schedule the pod with tolerations
kubectl create -f taints-and-tolerations/deployment-with-tolerations.yaml --save-config
```

```sh
# Check which node this pod was scheduled on
kgpn
```

```sh
# Add taint to the  worker
kubectl taint nodes advanced-scheduling-worker somekey=somevalue:NoExecute
```

```sh
# Check which pods are still running and where
kgpn
```

```sh
# Clean our doings
kubectl delete -f taints-and-tolerations/deployment-with-tolerations.yaml
kubectl delete -f taints-and-tolerations/deployment-without-tolerations.yaml
kubectl label nodes advanced-scheduling-worker workernumber-
kubectl taint nodes advanced-scheduling-worker somekey-
```

# NoSchedule (soft) Taints example
```sh
# Schedule the pod with tolerations
kubectl create -f taints-and-tolerations/deployment-without-tolerations.yaml --save-config
```

```sh
# Check which node this pod was scheduled on
kgpn
```

```sh
# Schedule the pod with tolerations
kubectl create -f taints-and-tolerations/deployment-with-tolerations.yaml --save-config
```

```sh
# Check which node this pod was scheduled on
kgpn
```

```sh
# Add taint to the second worker
kubectl taint nodes advanced-scheduling-worker somekey=somevalue:NoSchedule
```

```sh
# Check which pods are still running and where
kgpn
```
> Please note that no pods have been moved

```sh
# Now lets perform a a rolling update to our deployment
kubectl apply -f taints-and-tolerations/deployment-without-tolerations-alpine.yaml
```

```sh
# Check which pods are still running and where
kgpn
```
> Please note the deployment will fail, since the new pod cannot be scheduled. Thereof, the old pod will not be removed (always up!)

# Clean our doings
```sh
# Clean our doings
kubectl delete -f taints-and-tolerations/deployment-with-tolerations.yaml
kubectl delete -f taints-and-tolerations/deployment-without-tolerations.yaml
kubectl delete -f taints-and-tolerations/deployment-without-tolerations-alpine.yaml
kubectl label nodes advanced-scheduling-worker workernumber-
kubectl taint nodes advanced-scheduling-worker somekey-
```