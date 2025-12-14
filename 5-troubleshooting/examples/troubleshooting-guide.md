# Troubleshooting Guide

## Strategy
1.  **Isolate**: Is it a Pod, Node, or Cluster issue?
2.  **Describe**: Use `kubectl describe` to get events.
3.  **Logs**: Check pod logs (`kubectl logs`) and system logs (`journalctl`).

## Cheatsheet

### Pod Issues
- `kubectl get pods -A` -> Check status (Pending, CrashLoopBackOff, ImagePullBackOff).
- `kubectl describe pod <pod-name>` -> Check Events section.
- `kubectl logs <pod-name> [-c <container-name>]` -> Application errors.

### Node Issues
- `kubectl get nodes` -> Check status (NotReady).
- `kubectl describe node <node-name>` -> Resource pressure?
- `systemctl status kubelet` -> Is kubelet running?
- `journalctl -u kubelet` -> Kubelet logs.

### Control Plane Issues
- Check static pods in `/etc/kubernetes/manifests`.
- Check logs of api-server, scheduler, controller-manager.
- `crictl ps` -> Check if containers are running.

### Networking Issues
- Check CNI plugin pods (`kubectl get pods -n kube-system`).
- Check DNS (`nslookup kubernetes.default`).
- Check NetworkPolicies.
