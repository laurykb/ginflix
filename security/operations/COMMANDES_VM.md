# Commandes sur la VM

`172.18.0.200` = IP qu’on utilise pour joindre l’Ingress depuis la VM (MetalLB / nginx selon ton setup).

## Vérifier l’app (HTTP)

```bash
for p in / /admin /api/videos; do
  code=$(curl -sS -o /dev/null -w "%{http_code}" -H "Host: ginflix10.gin-telecom.ovh" "http://172.18.0.200${p}" || true)
  echo "${p}:${code}"
done
```

## Cluster

```bash
kubectl get nodes
kubectl -n kube-system get pods | egrep "kube-controller-manager|kube-scheduler|metrics-server"
kubectl -n ginflix get pods -o wide
```

## Manifests déployés (aperçu)

```bash
kubectl -n ginflix get deploy backend frontend frontend-admin streamer -o yaml
```

## Verification ingress headers

```bash
curl -sS -I -H "Host: ginflix10.gin-telecom.ovh" http://172.18.0.200/ | grep -Ei "x-frame-options|x-content-type-options|content-security-policy|permissions-policy|referrer-policy"
```

## Lister les dossiers de rapports

```bash
cd ~/ginflix/security/reports
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```
