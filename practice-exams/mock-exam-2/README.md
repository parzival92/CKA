# Mock Exam 2

## Instructions
- **Time Limit**: 2 hours
- **Passing Score**: 66%
- **Focus**: Troubleshooting & Networking

## Questions (Sample)

1.  **Context**: Node `worker-1`.
    **Task**: The node is `NotReady`. Fix the issue and make it `Ready`.

2.  **Context**: Cluster `k8s`.
    **Task**: Create a NetworkPolicy named `deny-all` in namespace `secure` that denies all ingress traffic.

3.  **Context**: Cluster `k8s`.
    **Task**: Upgrade the control plane to version `1.29.1`.

4.  **Context**: Cluster `k8s`.
    **Task**: Backup etcd to `/tmp/etcd-backup.db`.

## Grading
- Verify node status.
- Verify network connectivity (should be blocked).
- Verify version `kubectl get nodes`.
- Verify backup file exists.
