# kuberenetes-advanced-scheduling

# normaly deployed pod:
```sh
kubectl apply -f smallCPUPod.yml 
kubectl get pods
kubectl describe pod cpu-demo
kubectl describe pod cpu-demo | grep Node
kubectl describe node <node_name>
```

# not deployed - CPU to high
```sh
kubectl apply -f bigCPUPod.yml
kubectl get pods
kubectl describe pod cpu-demo-1
```

# crossing the limit 
```sh
kubectl apply -f crosingTheLimitPod.yml
kubectl get pods
kubectl exec -it pod/ubuntu -- /bin/bash
:(){ :|:& };:
```