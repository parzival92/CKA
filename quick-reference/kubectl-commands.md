# Quick kubectl Command Reference

## Cluster Information
```bash
kubectl cluster-info
kubectl config get-contexts
kubectl config use-context <context>
kubectl config current-context
kubectl version
```

## Nodes
```bash
kubectl get nodes
kubectl describe node <node-name>
kubectl top nodes
kubectl cordon <node-name>          # Prevent new pods
kubectl uncordon <node-name>        # Allow new pods
kubectl drain <node-name>           # Evict pods and prevent scheduling
```

## Pods
```bash
kubectl get pods
kubectl get pods -o wide
kubectl get pods -n <namespace>
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container>
kubectl exec -it <pod-name> -- /bin/bash
kubectl delete pod <pod-name>
```

## Deployments
```bash
kubectl create deployment <name> --image=<image>
kubectl get deployments
kubectl describe deployment <name>
kubectl scale deployment <name> --replicas=3
kubectl set image deployment/<name> <container>=<image>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>
```

## Services
```bash
kubectl expose deployment <name> --port=80 --target-port=8080
kubectl get svc
kubectl describe svc <name>
kubectl port-forward svc/<name> 8080:80
```

## Manifests
```bash
kubectl apply -f <file.yaml>
kubectl apply -f <directory>
kubectl create -f <file.yaml>
kubectl delete -f <file.yaml>
kubectl get <resource> -o yaml
kubectl edit <resource> <name>
```

## Debugging
```bash
kubectl get events
kubectl describe <resource> <name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- bash
kubectl port-forward <pod-name> 8080:80
kubectl top pods
kubectl top nodes
```

## Useful Aliases
```bash
alias k=kubectl
alias kg='kubectl get'
alias kd='kubectl describe'
alias kl='kubectl logs'
alias ke='kubectl exec -it'
alias ka='kubectl apply'
```
