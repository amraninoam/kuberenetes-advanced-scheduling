# kuberenetes-advanced-scheduling

# normaly deployed pod:
kubectl apply -f smallCPUPod.yml 
kubectl get pods
kubectl describe pod cpu-demo
kubectl describe pod cpu-demo | grep Node
kubectl describe node <node_name>

# not deployed - CPU to high
kubectl apply -f bigCPUPod.yml
kubectl get pods
kubectl describe pod cpu-demo-1

# crossing the limit 
kubectl apply -f crosingTheLimitPod.yml
kubectl get pods
kukbectl exec -it ubuntu -- /bin/bash
:(){ :|:& };: