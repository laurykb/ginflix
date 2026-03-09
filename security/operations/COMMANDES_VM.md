# Commandes VM de reference

## Verification service

```bash
for p in / /admin /api/videos; do
  code=$(curl -sS -o /dev/null -w "%{http_code}" -H "Host: ginflix10.gin-telecom.ovh" "http://172.18.0.200${p}" || true)
  echo "${p}:${code}"
done
```

## Verification cluster

```bash
kubectl get nodes
kubectl -n kube-system get pods | egrep "kube-controller-manager|kube-scheduler|metrics-server"
kubectl -n ginflix get pods -o wide
```

## Verification hardening workloads

```bash
kubectl -n ginflix get deploy backend frontend frontend-admin streamer -o yaml
```

## Verification ingress headers

```bash
curl -sS -I -H "Host: ginflix10.gin-telecom.ovh" http://172.18.0.200/ | grep -Ei "x-frame-options|x-content-type-options|content-security-policy|permissions-policy|referrer-policy"
```

## Index des rapports

```bash
cd ~/ginflix/security/reports
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```
