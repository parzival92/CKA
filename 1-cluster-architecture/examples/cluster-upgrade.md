# Cluster Upgrade Practice

## Objective
Perform a version upgrade of the Kubernetes cluster using `kubeadm`.

## Scenario
Upgrade the control plane and worker nodes from version `1.29.0` to `1.29.1` (or any available patch version).

## Steps

### 1. Upgrade Control Plane Node

```bash
# Drain the node
kubectl drain <control-plane-node> --ignore-daemonsets

# Update kubeadm
apt-get update && apt-get install -y kubeadm=1.29.1-00

# Verify plan
kubeadm upgrade plan

# Apply upgrade
sudo kubeadm upgrade apply v1.29.1

# Update kubelet and kubectl
apt-get install -y kubelet=1.29.1-00 kubectl=1.29.1-00
sudo systemctl daemon-reload
sudo systemctl restart kubelet

# Uncordon node
kubectl uncordon <control-plane-node>
```

### 2. Upgrade Worker Nodes

```bash
# Drain the node
kubectl drain <worker-node> --ignore-daemonsets

# Update kubeadm
apt-get update && apt-get install -y kubeadm=1.29.1-00

# Upgrade node config
sudo kubeadm upgrade node

# Update kubelet and kubectl
apt-get install -y kubelet=1.29.1-00 kubectl=1.29.1-00
sudo systemctl daemon-reload
sudo systemctl restart kubelet

# Uncordon node
kubectl uncordon <worker-node>
```
