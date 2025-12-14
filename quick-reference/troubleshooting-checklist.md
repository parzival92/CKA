# Troubleshooting Checklist

## Pod Troubleshooting

### Pod is Pending
- [ ] Check node availability: `kubectl get nodes`
- [ ] Check node selector: `kubectl describe pod <pod>`
- [ ] Check resource requests: `kubectl top nodes`
- [ ] Check taints and tolerations: `kubectl describe node <node>`
- [ ] Check PVC status if using storage: `kubectl get pvc`

### Pod is CrashLoopBackOff
- [ ] Check logs: `kubectl logs <pod>`
- [ ] Check previous logs: `kubectl logs <pod> --previous`
- [ ] Check events: `kubectl describe pod <pod>`
- [ ] Check resource limits: Are they too low?
- [ ] Check image: Does it exist and is it correct?

### Pod is ImagePullBackOff
- [ ] Verify image name: `kubectl describe pod <pod>`
- [ ] Check image registry credentials: `kubectl get secrets`
- [ ] Verify image exists in registry
- [ ] Check image pull policy

### Pod is in Running but not ready
- [ ] Check liveness probe: `kubectl describe pod <pod>`
- [ ] Check readiness probe: `kubectl describe pod <pod>`
- [ ] Check logs: `kubectl logs <pod>`
- [ ] Check if container started: `kubectl describe pod <pod>`

## Service Troubleshooting

### Service not accessible
- [ ] Check service exists: `kubectl get svc`
- [ ] Check endpoints: `kubectl get endpoints <service>`
- [ ] Check service type: ClusterIP, NodePort, LoadBalancer?
- [ ] Check pod selector matches pods: `kubectl get pods --selector=<selector>`
- [ ] Check port mapping: `kubectl describe svc <service>`

### DNS not resolving
- [ ] Check CoreDNS pods: `kubectl get pods -n kube-system`
- [ ] Check service DNS name: `kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup <service>`
- [ ] Check kube-dns config: `kubectl describe configmap coredns -n kube-system`

### Connection refused
- [ ] Check port-forward: `kubectl port-forward svc/<service> 8080:80`
- [ ] Check network policies: `kubectl get networkpolicies`
- [ ] Check firewall rules
- [ ] Check if service ports are correct

## Node Troubleshooting

### Node is NotReady
- [ ] SSH to node and check kubelet: `systemctl status kubelet`
- [ ] Check node logs: `kubectl describe node <node>`
- [ ] Check disk space: `df -h`
- [ ] Check memory: `free -m`
- [ ] Restart kubelet: `systemctl restart kubelet`

### Node is SchedulingDisabled
- [ ] Uncordon node: `kubectl uncordon <node>`
- [ ] Check if drained: `kubectl describe node <node>`

### High resource usage
- [ ] Check top pods: `kubectl top pods`
- [ ] Check top nodes: `kubectl top nodes`
- [ ] Identify resource hogs
- [ ] Increase resources or scale horizontally

## Cluster Troubleshooting

### Control plane issues
- [ ] Check control plane pods: `kubectl get pods -n kube-system`
- [ ] Check etcd: `kubectl describe pod -n kube-system etcd-<node>`
- [ ] Check API server: `kubectl get pods -n kube-system`
- [ ] Check scheduler: `kubectl get pods -n kube-system`
- [ ] Check controller-manager: `kubectl get pods -n kube-system`

### etcd issues
- [ ] Backup etcd: `ETCDCTL_API=3 etcdctl --endpoints 127.0.0.1:2379 snapshot save backup.db`
- [ ] Check etcd status
- [ ] Check etcd leader
- [ ] Review etcd logs

## Debugging Commands

```bash
# Get detailed pod info
kubectl describe pod <pod-name>

# View logs
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container>
kubectl logs <pod-name> --previous

# Interactive debugging
kubectl exec -it <pod-name> -- /bin/bash

# Port forwarding
kubectl port-forward <pod-name> 8080:80

# Get all events
kubectl get events --sort-by='.lastTimestamp'

# Cluster dump
kubectl cluster-info dump

# Check resource usage
kubectl top nodes
kubectl top pods
```

## Common Solutions

| Issue | Solution |
|-------|----------|
| Pod won't start | Check logs, image, resources |
| Service unreachable | Check endpoints, network policies |
| Node NotReady | Restart kubelet, check resources |
| DNS not working | Check CoreDNS, check service name |
| Storage issues | Check PVC, PV, storage class |
