# Troubleshooting (30%)

This section covers diagnosing and fixing Kubernetes cluster issues (30% of exam weight).

## Topics Covered

- **Cluster Issues**: Control plane problems, node failures, etcd issues
- **Pod Debugging**: Pod status, events, logs
- **Networking Issues**: DNS, service connectivity, network policies
- **Application Troubleshooting**: Container crashes, resource limits
- **Performance Issues**: Node resource usage, pod scheduling failures
- **Log Analysis**: Kubectl logs, system logs

## Key Commands

```bash
# Pod status and debugging
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>
kubectl logs <pod-name> --previous

# Interactive debugging
kubectl exec -it <pod-name> -- /bin/bash
kubectl port-forward <pod-name> 8080:80

# Node troubleshooting
kubectl get nodes
kubectl describe node <node-name>
kubectl top nodes
kubectl top pods

# Events
kubectl get events
kubectl describe events

# Cluster diagnostics
kubectl cluster-info
kubectl cluster-info dump
```

## Common Issues

1. **CrashLoopBackOff**: Check logs and events
2. **Pending**: Check node resources and node selectors
3. **ImagePullBackOff**: Verify image name and registry credentials
4. **Connection Refused**: Check service endpoints and network policies

## Resources

- [Troubleshooting Documentation](https://kubernetes.io/docs/tasks/debug-application-cluster/)
- [Debugging Services](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/)

## Practice

See `scenarios/` folder for troubleshooting scenarios and `examples/` for common issues.
