# EKS Troubleshooting Notes

## Deployment Health

```bash
kubectl get pods -n devops-demo
kubectl describe pod <pod-name> -n devops-demo
kubectl logs <pod-name> -n devops-demo
kubectl rollout status deployment/webapp -n devops-demo
```

## HPA Issues

```bash
kubectl get hpa -n devops-demo
kubectl describe hpa webapp -n devops-demo
kubectl top pods -n devops-demo
kubectl get deployment metrics-server -n kube-system
```

If HPA target shows `unknown`, check Metrics Server, resource requests, and RBAC permissions.

## Rollback Scenario

If a new image causes `CrashLoopBackOff`, verify logs and roll back:

```bash
helm history webapp -n devops-demo
helm rollback webapp <revision> -n devops-demo
```
