# Requests and Limits

## Pod request 1 cpu
```sh
# Schedule the pod with 1 CPU request
kubectl create -f pod-1-CPU-request.yml --save-config
```
```sh
# Check the pod is up and running
kubectl get pods
kubectl describe pod pod1cpu
```
```sh
# Check the node the pod is running on
kubectl describe pod pod1cpu | grep Node
kubectl describe node <node_name>
```

## Pod request 80 cpus
```sh
# Schedule the pod with 80 CPUs request
kubectl create -f pod-80-CPUs-request.yml --save-config
```
```sh
# Check if the Pod is running and see describe for more info
kubectl get pods
kubectl describe pod pod80cpus
```

## Clean our doings
```sh
# Clean our doings
kubectl delete -f pod-80-CPUs-request.yml
kubectl delete -f pod-1-CPU-request.yml
```

## Installing metrics server for watching pod memory and CPU
```sh
# Install a metrics server for watching pods CPU and memory usage
kubectl create -f metrics-server.yaml --save-config
```
```sh
# Check if its running
kubectl get deployment metrics-server -n kube-system 
```

## Crossing the CPU limit 
```sh
# Schedule the pod with 100m CPU Limit
kubectl create -f pod-CPU-limit.yml --save-config
```
```sh
# check the pod is running
kubectl get pods
```
```sh
# Open a new terminal for watching the pods CPU usage
kubectl top pod ubuntucpu
```
```sh
# "Drop" the fork Bomb and see what happens to the CPU
kubectl exec -it pod/ubuntucpu -- /bin/bash
:(){ :|:& };:
```

## Change the Limit to 200 and watch what happens
- Inside pod-CPU-limit.yml change row no.14 to 200 and save
```sh
# Schedule the pod with 200m CPU Limit
kubectl apply -f pod-CPU-limit.yml
```
```sh 
# check the pod is running
kubectl get pods
```
```sh
# Open a new terminal for watching the pods CPU usage
kubectl top pod ubuntucpu
```
```sh
# "Drop" the fork Bomb and see what happens to the CPU
kubectl exec -it pod/ubuntucpu -- /bin/bash
:(){ :|:& };:
```

## Crossing the memory limit
```sh
# Schedule the pod with 100Mib memory Limit
kubectl create -f pod-memory-limit.yml --save-config
```
```sh
# check the pod is running
kubectl get pods
```
```sh
# Open a new terminal for watching the pods memory usage
kubectl top pod ubuntumemory
```
```sh
# "Drop" the fork Bomb and see what happens to the memory
kubectl exec -it pod/ubuntumemory -- /bin/bash
:(){ :|:& };:
```

## Clean our doings
```sh
# Clean our doings
kubectl delete -f pod-memory-limit.yml
kubectl delete -f pod-CPU-limit.yml
kubectl delete -f metrics-server.yaml
```