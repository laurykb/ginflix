# GINFLIX

Projet etudiant de plateforme video deployee sur Kubernetes in Docker.

## Lecture rapide

1. `security/README.md`
2. `security/STATUS.md`
3. `security/RESULTATS.md`

## Arborescence utile

- `namespace/`: namespace et base du cluster.
- `backend/`, `frontend/`, `streamer/`, `database/`: composants applicatifs.
- `ingress/`, `loadbalancer/`, `service-nodeport/`: exposition reseau.
- `CiliumNetworkPolicies/`: segmentation reseau.
- `metrics-server/`: prerequis HPA.
- `secret/`: exemples de secrets Kubernetes.
- `security/`: documentation et preuves.

## Fichiers centraux

- `config-map-ginflix.yaml`: ConfigMap principale.
- `kind-cilium.yaml`: cluster Kind avec Cilium.
- `.github/workflows/security-gitleaks.yml`: scan secrets en CI.
- `.github/workflows/security-kics.yml`: scan IaC en CI.

## Outils securite retenus

- `Trivy`
- `Gitleaks`
- `KICS`
