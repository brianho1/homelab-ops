# cert-monitor

Helm chart that deploys a weekly Kubernetes CronJob to check RKE2 certificate
expiry and send alerts via ntfy.

## Sealing the ntfy token

Run once to generate the SealedSecret (requires `kubeseal` and cluster access):

```bash
# 1. Create a temp secret file (never commit this)
kubectl create secret generic cert-monitor-ntfy \
  --namespace cert-monitor \
  --from-literal=NTFY_TOKEN=<your-token> \
  --dry-run=client -o yaml > /tmp/ntfy-secret.yaml

# 2. Seal it against the cluster
kubeseal --controller-name=sealed-secrets-controller \
  --controller-namespace=kube-system \
  --format yaml < /tmp/ntfy-secret.yaml > templates/sealedsecret.yaml

# 3. Clean up
rm /tmp/ntfy-secret.yaml
```

## Schedule

Default: every Monday at 9am (`0 9 * * 1`). Override in `values.yaml`.

## Alert threshold

Default: 60 days before expiry. Override `warnDays` in `values.yaml`.
