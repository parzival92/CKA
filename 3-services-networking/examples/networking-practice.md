# Networking Practice

## Objective
Master Services, Ingress, and Network Policies.

## Concepts

### 1. Services
- **ClusterIP**: Internal communication.
- **NodePort**: Expose on static port on each node.
- **DNS**: Services get DNS names `<service-name>.<namespace>.svc.cluster.local`.

### 2. Ingress
- Layer 7 routing (HTTP/HTTPS).
- Requires an Ingress Controller (e.g., Nginx) to be running.

### 3. Network Policies
- Controls traffic between pods.
- **Default**: All traffic allowed.
- **Best Practice**: Start with "Deny All" and allow necessary paths.

## Practice Scenarios

### Scenario 1: Service Discovery
1.  Create a Deployment `nginx` with 2 replicas.
2.  Expose it via a Service `nginx-svc` (ClusterIP).
3.  Run a temporary pod: `kubectl run tmp --image=busybox --restart=Never --rm -it -- sh`.
4.  Inside the pod, test DNS: `nslookup nginx-svc`.

### Scenario 2: Secure the Backend
1.  Create `frontend` and `backend` pods.
2.  Apply a NetworkPolicy that denies all ingress to `backend`.
3.  Verify `frontend` cannot reach `backend`.
4.  Update policy to allow traffic ONLY from `frontend`.
5.  Verify connectivity is restored.

### Scenario 3: Ingress Routing
1.  Deploy an Ingress Controller (if not present).
2.  Create two services: `blue-svc` and `green-svc`.
3.  Create an Ingress resource that routes `/blue` to `blue-svc` and `/green` to `green-svc`.
