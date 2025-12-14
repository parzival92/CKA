# LoadBalancer Service Example

## What is a LoadBalancer Service?

A **LoadBalancer** service exposes your application **externally** to the internet/network. It assigns an external IP that anyone outside the cluster can use to access your app.

### When to Use:
- Web applications
- Public APIs
- Customer-facing services
- Any service needing external access

---

## Complete Example: NGINX Web Server with LoadBalancer

### What We'll Create:
1. An **NGINX Deployment** - Web server
2. A **Service (LoadBalancer)** - Exposes to external world
3. Access from outside the cluster

---

## Step 1: Create NGINX Deployment YAML

**File: nginx-deployment.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
    tier: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "64Mi"
            cpu: "100m"
          limits:
            memory: "128Mi"
            cpu: "200m"
```

**What this does:**
- Creates 3 NGINX pods (replicas: 3)
- Exposes port 80
- Defines resource requests and limits
- Uses default nginx image with index.html

---

## Step 2: Create LoadBalancer Service YAML

**File: nginx-service.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-lb
  labels:
    app: nginx
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30007
```

**What this does:**
- Creates a service named "nginx-lb"
- Type: LoadBalancer (external access)
- Selects pods with label `app: nginx`
- Port 80 (external) → Pod port 80 (internal)
- nodePort: 30007 (optional, specific port on nodes)

---

## Comparing ClusterIP vs LoadBalancer

| Feature | ClusterIP | LoadBalancer |
|---------|-----------|--------------|
| Access | Internal only | External + Internal |
| IP Type | Cluster-internal | External IP |
| Visible | Only inside cluster | From anywhere |
| Use Case | Databases, caches | Web apps, APIs |
| Port | Any | Cloud provider dependent |

### YAML Comparison:

**ClusterIP:**
```yaml
spec:
  type: ClusterIP
  # No external IP
```

**LoadBalancer:**
```yaml
spec:
  type: LoadBalancer
  # Gets external IP
```

---

## Step 3: How to Use - Commands

### 1. Create the resources
```bash
# Create NGINX deployment
kubectl apply -f nginx-deployment.yaml

# Create LoadBalancer service
kubectl apply -f nginx-service.yaml
```

### 2. Verify the service
```bash
# List all services
kubectl get svc

# OUTPUT:
# NAME         TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
# nginx-lb     LoadBalancer   10.96.15.45   203.0.113.100   80:30007/TCP   2m
#                                           ↑ EXTERNAL IP!
```

### 3. Check service details
```bash
kubectl describe svc nginx-lb

# OUTPUT:
# Name:                     nginx-lb
# Namespace:                default
# Labels:                   app=nginx
# Annotations:              <none>
# Selector:                 app=nginx
# Type:                     LoadBalancer
# IP:                       10.96.15.45
# Port:                     <unset>  80/TCP
# TargetPort:               80/TCP
# NodePort:                 30007/TCP
# Endpoints:                172.17.0.2:80,172.17.0.3:80,172.17.0.4:80
# LoadBalancer Ingress:     203.0.113.100
```

### 4. Check endpoints (which pods are running)
```bash
kubectl get endpoints nginx-lb

# OUTPUT:
# NAME       ENDPOINTS                                      AGE
# nginx-lb   172.17.0.2:80,172.17.0.3:80,172.17.0.4:80    2m
```

### 5. Access the service from outside
```bash
# Using External IP
curl http://203.0.113.100

# Or using localhost (for local clusters like minikube)
curl http://localhost:80

# OUTPUT:
# <!DOCTYPE html>
# <html>
# <head>
#   <title>Welcome to nginx!</title>
# ...
```

### 6. Check pods are running
```bash
kubectl get pods -l app=nginx

# OUTPUT:
# NAME                               READY   STATUS    RESTARTS   AGE
# nginx-deployment-5d59d67564-abc12  1/1     Running   0          3m
# nginx-deployment-5d59d67564-def45  1/1     Running   0          3m
# nginx-deployment-5d59d67564-ghi78  1/1     Running   0          3m
```

---

## Understanding Traffic Flow

### With LoadBalancer:

```
Internet User
    ↓ (203.0.113.100:80)
External Load Balancer
    ↓ (distributes traffic)
Node 1 Port 30007 → Pod 1 (nginx) Port 80
Node 2 Port 30007 → Pod 2 (nginx) Port 80
Node 3 Port 30007 → Pod 3 (nginx) Port 80
```

### Ports Explained:

1. **Port 80** - External access port (what users use)
2. **TargetPort 80** - Port inside container
3. **NodePort 30007** - Host port (30000-32767 range)

---

## Local Testing (Minikube/Docker Desktop)

If running locally without a real load balancer:

```bash
# Method 1: Port forwarding
kubectl port-forward svc/nginx-lb 8080:80
# Access at http://localhost:8080

# Method 2: Using minikube
minikube service nginx-lb
# Automatically opens in browser

# Method 3: Using NodePort
kubectl get svc nginx-lb
# Use: http://localhost:<NODEPORT>
```

---

## Example: Multi-Port LoadBalancer

If your app has multiple ports (HTTP and HTTPS):

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-multi-lb
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
  - name: http
    port: 80
    targetPort: 80
  - name: https
    port: 443
    targetPort: 443
```

Access:
```bash
curl http://EXTERNAL-IP:80
curl https://EXTERNAL-IP:443
```

---

## Key Points

✅ **LoadBalancer Summary:**
- Accessible from outside cluster
- Gets external IP address
- Can be accessed by anyone with external IP
- Great for public services
- May incur cloud charges

❌ **Limitations:**
- Not all providers support it (only cloud/local)
- Slower than ClusterIP
- More expensive

---

## Cleanup

```bash
# Delete the resources
kubectl delete -f nginx-service.yaml
kubectl delete -f nginx-deployment.yaml

# Or delete all at once
kubectl delete -f .
```

---

## Real-World Analogy

Think of LoadBalancer like a **public phone number**:
- Anyone can call it from anywhere
- Gets distributed to multiple lines
- Public number on the internet
- More expensive than internal extension
