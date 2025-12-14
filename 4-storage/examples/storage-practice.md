# Storage Practice

## Objective
Understand how to manage persistent storage in Kubernetes.

## Concepts

### 1. PersistentVolume (PV)
- A piece of storage in the cluster.
- Can be provisioned statically (admin creates PV) or dynamically (StorageClass).

### 2. PersistentVolumeClaim (PVC)
- A request for storage by a user.
- Pods use PVCs as volumes.

### 3. StorageClass
- Defines "classes" of storage (e.g., fast-ssd, slow-hdd).
- Enables dynamic provisioning.

## Practice Scenarios

### Scenario 1: Static Provisioning
1.  Create a `hostPath` PV with 1Gi capacity.
2.  Create a PVC requesting 500Mi.
3.  Verify the PVC binds to the PV (`Bound` status).
4.  Create a Pod that mounts this PVC to `/data`.
5.  Write a file to `/data` in the pod, delete the pod, recreate it, and verify the file exists.

### Scenario 2: Storage Class
1.  Check available storage classes: `kubectl get sc`.
2.  Create a PVC specifying a valid `storageClassName`.
3.  Verify a PV is automatically created.
