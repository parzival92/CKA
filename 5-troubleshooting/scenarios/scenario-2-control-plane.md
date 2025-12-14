# Scenario 2: Control Plane Failure

## Problem
`kubectl` commands are failing or timing out.

## Simulation
(Run this on the control plane node)
```bash
# Move scheduler manifest
sudo mv /etc/kubernetes/manifests/kube-scheduler.yaml /tmp/
```

## Diagnosis Steps
1.  `kubectl get pods -n kube-system` -> Is scheduler running?
2.  Try to schedule a new pod. It should stay `Pending`.
3.  Check `/etc/kubernetes/manifests` folder.

## Fix
Restore the manifest.
```bash
sudo mv /tmp/kube-scheduler.yaml /etc/kubernetes/manifests/
```
