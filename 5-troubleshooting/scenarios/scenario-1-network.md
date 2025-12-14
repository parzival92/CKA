# Scenario 1: Network Failure

## Problem
Pods cannot communicate with each other or resolve DNS names.

## Simulation
(Run this on a worker node to break it)
```bash
# Break CNI
sudo mv /etc/cni/net.d/10-flannel.conflist /tmp/
```

## Diagnosis Steps
1.  `kubectl get pods -o wide` -> Are pods stuck in `ContainerCreating`?
2.  `kubectl describe pod <pod-name>` -> Look for "FailedCreatePodSandBox".
3.  Check CNI configuration in `/etc/cni/net.d/`.

## Fix
Restore the CNI configuration file.
```bash
sudo mv /tmp/10-flannel.conflist /etc/cni/net.d/
```
