# ClusterIP Service Example

## What is a ClusterIP Service?

A **ClusterIP** is a Kubernetes service that exposes your application **internally** within the cluster only. It assigns an internal IP address that is accessible from within the cluster but not from outside.

### When to Use:
- Database services
- Internal APIs
- Caching services
- Any backend service accessed only by other pods

---

## Complete Example: MySQL Database Service

### Step 1: Understanding the Components

We'll create:
1. A **Deployment** - Runs MySQL container
2. A **Service (ClusterIP)** - Exposes MySQL internally
3. A **Test Pod** - Verifies connectivity

---

### Step 2: What YAML Means

**YAML** = Yet Another Markup Language
- A file format to define Kubernetes resources
- Uses indentation (spaces) to organize data
- Each resource has `kind`, `metadata`, `spec`, and `status`

Example structure:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  type: ClusterIP
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
```

Breaking it down:
- `apiVersion: v1` - API version
- `kind: Service` - Type of resource
- `metadata.name` - Name of the service
- `spec.type: ClusterIP` - Service type (internal only)
- `spec.selector` - Which pods to expose (must match pod labels)
- `spec.ports` - Port mapping

---

### Step 3: Create MySQL Deployment YAML

**File: mysql-deployment.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  labels:
    app: mysql
    tier: database
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
        tier: database
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        ports:
        - containerPort: 3306
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: "password123"
        - name: MYSQL_DATABASE
          value: "mydb"
        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-storage
        emptyDir: {}
```

**What this does:**
- Creates 1 MySQL pod (replica: 1)
- Exposes port 3306
- Sets root password to "password123"
- Creates database "mydb"
- Uses temporary storage (emptyDir)

---

### Step 4: Create ClusterIP Service YAML

**File: mysql-service.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
  labels:
    app: mysql
spec:
  type: ClusterIP
  selector:
    app: mysql
  ports:
  - protocol: TCP
    port: 3306
    targetPort: 3306
```

**What this does:**
- Creates a service named "mysql-service"
- Type: ClusterIP (internal only)
- Selects pods with label `app: mysql` (matches deployment)
- Port 3306 inside cluster → Pod port 3306

---

## Step 5: How to Use - Commands

### 1. Create the resources
```bash
# Create MySQL deployment
kubectl apply -f mysql-deployment.yaml

# Create MySQL service
kubectl apply -f mysql-service.yaml
```

### 2. Verify the service
```bash
# List all services
kubectl get svc

# OUTPUT:
# NAME              TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
# mysql-service     ClusterIP   10.96.45.123    <none>        3306/TCP   5m

# <none> = Not accessible from outside cluster (internal only)
```

### 3. Check service details
```bash
kubectl describe svc mysql-service

# OUTPUT:
# Name:              mysql-service
# Namespace:         default
# Labels:            app=mysql
# Annotations:       <none>
# Selector:          app=mysql
# Type:              ClusterIP
# IP:                10.96.45.123
# Port:              <unset>  3306/TCP
# TargetPort:        3306/TCP
# Endpoints:         172.17.0.3:3306
```

### 4. Check endpoints (which pods are connected)
```bash
kubectl get endpoints mysql-service

# OUTPUT:
# NAME              ENDPOINTS          AGE
# mysql-service     172.17.0.3:3306    5m
```

### 5. Test from another pod
```bash
# Create a test pod and connect to MySQL service
kubectl run -it --rm mysql-client --image=mysql:5.7 --restart=Never -- \
  mysql -h mysql-service -u root -ppassword123 -e "SELECT 1;"

# OUTPUT:
# +---+
# | 1 |
# +---+
# | 1 |
# +---+
```

---

## Understanding DNS Resolution

Inside the cluster, Kubernetes has DNS. You can access the service by name:

```bash
# Access using service name
mysql -h mysql-service -u root -ppassword123

# Access using FQDN (Fully Qualified Domain Name)
mysql -h mysql-service.default.svc.cluster.local -u root -ppassword123

# Format: <service-name>.<namespace>.svc.cluster.local
```

---

## Key Points

✅ **ClusterIP Summary:**
- Internal IP only (not accessible from outside)
- All pods can reach it using service name
- Most secure for internal services
- No external IP assigned

❌ **Cannot do:**
- Access from outside the cluster
- No external IP address

---

## Cleanup

```bash
# Delete the resources
kubectl delete -f mysql-service.yaml
kubectl delete -f mysql-deployment.yaml

# Or delete all at once
kubectl delete -f .
```

---

## Real-World Analogy

Think of ClusterIP like an **internal phone extension in an office**:
- Only people in the office can call it
- Has an internal extension number
- Cannot be called from outside
- Perfect for internal communication
