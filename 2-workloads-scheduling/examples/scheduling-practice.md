# Scheduling Practice

## Objective
Master advanced scheduling techniques including Taints, Tolerations, and Node Affinity.

## Concepts

### 1. Taints and Tolerations
- **Taints** are applied to Nodes. They repel pods.
- **Tolerations** are applied to Pods. They allow (but don't require) pods to schedule onto tainted nodes.

**Command to taint a node:**
```bash
kubectl taint nodes node1 key=value:NoSchedule
```

**Pod Toleration:**
```yaml
tolerations:
- key: "key"
  operator: "Equal"
  value: "value"
  effect: "NoSchedule"
```

### 2. Node Affinity
- Constrains which nodes your pod is eligible to be scheduled on, based on labels on the node.

**Label a node:**
```bash
kubectl label nodes node1 disktype=ssd
```

## Practice Scenarios

### Scenario 1: Dedicated Node
1.  Taint `node01` with `env=prod:NoSchedule`.
2.  Try to deploy a standard Nginx pod. Verify it stays `Pending`.
3.  Add a toleration to the pod spec. Verify it schedules.

### Scenario 2: SSD Preference
1.  Label `node01` with `disk=ssd` and `node02` with `disk=hdd`.
2.  Create a Deployment that *prefers* `disk=ssd`.
3.  Scale the deployment and observe distribution.

### Scenario 3: Static Pods
1.  Navigate to `/etc/kubernetes/manifests` on a node.
2.  Create a Pod manifest there.
3.  Verify the Mirror Pod is created by the Kubelet.
