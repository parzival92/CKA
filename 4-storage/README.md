# Storage (10%)

This section covers persistent storage in Kubernetes.

## Topics Covered

- **Volumes**: emptyDir, hostPath, configMap, secret
- **Persistent Volumes (PV)**: Storage provisioning and lifecycle
- **Persistent Volume Claims (PVC)**: Storage consumption
- **Storage Classes**: Dynamic provisioning
- **Snapshots & Backups**: Data persistence strategies

## Key Commands

```bash
# Persistent Volumes
kubectl get pv
kubectl describe pv <pv-name>

# Persistent Volume Claims
kubectl get pvc
kubectl describe pvc <pvc-name>

# Storage Classes
kubectl get storageclass
kubectl describe storageclass <sc-name>

# Create PVC
kubectl apply -f pvc.yaml
```

## Key Concepts

- **Access Modes**: ReadWriteOnce, ReadOnlyMany, ReadWriteMany
- **Reclaim Policy**: Retain, Delete, Recycle
- **Storage Provisioning**: Static vs Dynamic

## Resources

- [Storage Documentation](https://kubernetes.io/docs/concepts/storage/)
- [Persistent Volumes Documentation](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

## Practice

See `examples/` folder for YAML manifests and `yaml-files/` for templates.
