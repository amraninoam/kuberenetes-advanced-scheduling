# Taints and Tolerations
## Set Aliases
Add these aliases to your session
```sh
alias kgpn='kubectl get pods -o jsonpath='"'"'{range .items[*]}{@.metadata.name}{" "}{@.spec.nodeName}{"\n"}{end}'"'"''
alias kgnot='kubectl get nodes -o jsonpath='"'"'{range .items[*]}{@.metadata.name}{" "}{@.spec.taints[*].key}:{@.spec.taints[*].value}-{@.spec.taints[*].effect}{"\n"}{end}'"'"''
```


## Label the second worker
Add label to the second worker, so our pod will be scheduled on it (using selector)
```sh
kubectl label nodes advanced-scheduling-worker2 workernumber=2
```

## Schedulg workload
Schedule the pod with tolerations
```sh
kubectl create -f taints-and-tolerations/deployment-without-tolerations.yaml
```

Check which node this pod was scheduled on
```sh
kgpn
```

Schedule the pod with tolerations
```sh
kubectl create -f taints-and-tolerations/deployment-with-tolerations.yaml
```

Check which node this pod was scheduled on
```sh
kgpn
```

Add taint to the second worker
```sh
kubectl taint nodes advanced-scheduling-worker2 somekey=somevalue:NoExecute
```

## Clean our doings
```sh
kubectl delete -f taints-and-tolerations/deployment-with-tolerations.yaml
kubectl delete -f taints-and-tolerations/deployment-without-tolerations.yaml
kubectl label nodes advanced-scheduling-worker2 workernumber-
kubectl taint nodes advanced-scheduling-worker2 somekey-
```