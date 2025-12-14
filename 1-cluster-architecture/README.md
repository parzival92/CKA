# Cluster Architecture, Installation & Configuration (25%)

This section covers the foundational concepts for setting up and managing Kubernetes clusters.

## Topics Covered

- **Cluster Installation**: kubeadm, managed services (EKS, AKS, GKE)
- **Node Management**: Worker nodes, control plane components
- **High Availability**: Multi-master setup, etcd backup/restore
- **Storage**: PersistentVolumes, PersistentVolumeClaims, StorageClasses
- **Networking Fundamentals**: Pod networking, CIDR, DNS

## Key Commands

```bash
# Cluster info
kubectl cluster-info
kubectl get nodes
kubectl describe node <node-name>

# Backup etcd
ETCDCTL_API=3 etcdctl --endpoints 127.0.0.1:2379 snapshot save backup.db

# Restore etcd
ETCDCTL_API=3 etcdctl --endpoints 127.0.0.1:2379 snapshot restore backup.db
```

## Resources

- [Official K8s Docs - Cluster Setup](https://kubernetes.io/docs/setup/)
- [kubeadm Documentation](https://kubernetes.io/docs/reference/setup-tools/kubeadm/)

## Practice

See `examples/` folder for YAML manifests and `yaml-files/` for templates.
