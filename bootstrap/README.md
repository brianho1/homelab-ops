# Bootstrap

One-time setup steps to bootstrap ArgoCD onto the cluster.
After this, everything else is managed via GitOps.

## 1. Install ArgoCD

```bash
kubectl apply -k bootstrap/argocd/
```

## 2. Wait for ArgoCD to be ready

```bash
kubectl wait --for=condition=available --timeout=300s deployment/argocd-server -n argocd
```

## 3. Get initial admin password

```bash
kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath="{.data.password}" | base64 -d && echo
```

## 4. Access ArgoCD UI

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
# Open https://localhost:8080, login: admin / <password above>
```

## 5. Apply app-of-apps

```bash
kubectl apply -f apps/app-of-apps.yaml
```
