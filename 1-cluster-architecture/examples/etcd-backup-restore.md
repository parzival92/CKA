# ETCD Backup and Restore Practice

## Objective
Learn how to backup and restore the etcd cluster, which is critical for recovering the state of your Kubernetes cluster.

## Prerequisites
- Access to a control plane node.
- `etcdctl` installed.
- Certificates for etcd authentication (usually found in `/etc/kubernetes/pki/etcd`).

## Scenario
1.  **Snapshot the current state**: Take a snapshot of the etcd database.
2.  **Simulate failure**: Delete a resource (e.g., a Deployment) to simulate data loss.
3.  **Restore**: Restore the etcd database from the snapshot.
4.  **Verify**: Check if the deleted resource is back.

## Commands

### 1. Take a Snapshot

```bash
ETCDCTL_API=3 etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save /tmp/etcd-backup.db
```

### 2. Verify Snapshot Status

```bash
ETCDCTL_API=3 etcdctl --write-out=table snapshot status /tmp/etcd-backup.db
```

### 3. Restore from Snapshot

**Note**: This usually requires stopping the static pod or the etcd service.

```bash
# Stop etcd (if running as static pod, move the manifest)
mv /etc/kubernetes/manifests/etcd.yaml /tmp/

# Restore
ETCDCTL_API=3 etcdctl snapshot restore /tmp/etcd-backup.db \
  --data-dir=/var/lib/etcd-from-backup

# Update etcd.yaml to point to new data-dir or move the restored data to /var/lib/etcd
# (Safer to update the manifest hostPath)
```

### 4. Restart Etcd
Move the manifest back:
```bash
mv /tmp/etcd.yaml /etc/kubernetes/manifests/
```
