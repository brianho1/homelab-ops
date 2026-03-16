# homelab-ops

GitOps repository for my homelab Kubernetes cluster (RKE2) managed with ArgoCD and Helm.

## Stack

- **Kubernetes:** RKE2 v1.30 — 3 masters, 5 workers (Intel NUCs)
- **GitOps:** ArgoCD
- **Packaging:** Helm
- **Secrets:** Sealed Secrets
- **Notifications:** ntfy (self-hosted)

## Structure

```
apps/          # ArgoCD Application manifests
charts/        # Helm charts
  cert-monitor/  # RKE2 certificate expiry monitoring + ntfy alerts
bootstrap/     # ArgoCD install + initial setup
```

## Bootstrap

See [bootstrap/README.md](bootstrap/README.md) for cluster setup instructions.
