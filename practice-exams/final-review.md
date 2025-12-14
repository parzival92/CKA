# Final Review Checklist

## Top Priority (Must Know)
- [ ] **Cluster Upgrade**: `kubeadm upgrade apply ...`
- [ ] **ETCD Backup/Restore**: `etcdctl snapshot save ...`
- [ ] **Troubleshooting**: Fix a broken node (kubelet) and a broken pod.
- [ ] **Network Policies**: Deny all, Allow specific.
- [ ] **PVC/PV**: Bind a PVC to a pod.

## Commands to Memorize
- `kubectl run ... --dry-run=client -o yaml`
- `kubectl create deploy ... --dry-run=client -o yaml`
- `kubectl expose ... --dry-run=client -o yaml`
- `kubectl explain pod.spec.containers.livenessProbe`

## Exam Day Tips
1.  **Context**: Always check which cluster you are on (`kubectl config current-context`).
2.  **Time**: Don't get stuck. Flag and move on.
3.  **Copy/Paste**: Use the official docs to copy YAML snippets.
