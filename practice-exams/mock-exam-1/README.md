# Mock Exam 1

## Instructions
- **Time Limit**: 2 hours
- **Passing Score**: 66%
- **Questions**: 15-20

## Setup
Ensure you have a clean cluster (or use a simulator like Killer.sh if you have access).

## Questions (Sample)

1.  **Context**: Cluster `k8s`.
    **Task**: Create a deployment named `nginx-deploy` with image `nginx:1.16` and 2 replicas. Expose it as a service `nginx-svc` on port 80.

2.  **Context**: Cluster `k8s`.
    **Task**: A pod named `web-pod` is failing. Fix the issue so it enters `Running` state.

3.  **Context**: Cluster `k8s`.
    **Task**: Create a PersistentVolume named `pv-log` with capacity `100Mi`, access mode `ReadWriteMany`, and host path `/pv/log`.

4.  **Context**: Cluster `k8s`.
    **Task**: Create a user `john` with certificates and give him `list` access to `pods` in `default` namespace.

## Grading
- 5 points per question.
- Check your work using `kubectl get` and `kubectl describe`.
