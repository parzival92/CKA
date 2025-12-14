# Workloads & Scheduling (15%)

This section covers running and managing workloads in Kubernetes, including scheduling policies.

## Topics Covered

- **Deployments**: Creating, updating, rolling back
- **StatefulSets**: Stateful applications, persistent identities
- **DaemonSets**: Running on every node
- **Jobs & CronJobs**: Batch processing, scheduled tasks
- **Scheduling**: Node affinity, pod affinity, taints, tolerations
- **Pod Resource Management**: Requests, limits, QoS

## Key Commands

```bash
# Deployments
kubectl create deployment <name> --image=<image>
kubectl set image deployment/<name> <container>=<image>
kubectl rollout history deployment/<name>
kubectl rollout undo deployment/<name>

# Scaling
kubectl scale deployment <name> --replicas=3

# StatefulSets
kubectl create statefulset <name> --image=<image>

# Jobs
kubectl create job <name> --image=<image> -- <command>

# Pod scheduling info
kubectl get pods -o wide
kubectl describe pod <pod-name>
```

## Resources

- [Deployments Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [StatefulSets Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
- [Scheduling Documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/)

## Practice

See `examples/` folder for YAML manifests and `yaml-files/` for templates.
