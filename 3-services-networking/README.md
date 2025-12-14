# Services & Networking (20%)

This section covers Kubernetes networking, services, and ingress configuration.

## Topics Covered

- **Service Types**: ClusterIP, NodePort, LoadBalancer, ExternalName
- **Ingress**: Ingress controllers, routing rules
- **Network Policies**: Pod-to-pod communication control
- **CoreDNS**: Service discovery, DNS configuration
- **CNI Plugins**: Container networking interface

## Key Commands

```bash
# Services
kubectl expose deployment <name> --port=80 --target-port=8080 --type=LoadBalancer
kubectl get svc
kubectl describe svc <service-name>

# Endpoints
kubectl get endpoints

# DNS resolution
kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup <service>

# Port forwarding
kubectl port-forward svc/<service> 8080:80

# Network policies
kubectl apply -f network-policy.yaml
kubectl get networkpolicies
```

## Resources

- [Services Documentation](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Ingress Documentation](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [Network Policies Documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

## Practice

See `examples/` folder for YAML manifests and `yaml-files/` for templates.
