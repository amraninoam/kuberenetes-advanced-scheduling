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

# installing metrics server for watching memory
```sh
kubectl apply -f components.yaml
kubectl get deployment metrics-server -n kube-system 
```

# crossing the limit 
```sh
kubectl apply -f crosingTheLimitPod.yml
kubectl top pod ubuntu
kubectl get pods
kubectl exec -it pod/ubuntu -- /bin/bash
:(){ :|:& };:
```

kubectl apply -f components.yaml
kubectl get deployment metrics-server -n kube-system 