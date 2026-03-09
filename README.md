# GINFLIX - Projet DevSecOps Kubernetes

Depot de projet etudiant (ecole d'ingenieur) pour deploiement d'une plateforme video sur Kubernetes, avec demarche DevSecOps documentee et auditable.

## Lecture recommandee

1. `security/README.md` (vue securite globale)
2. `security/STATUS.md` (etat d'avancement et decisions)
3. `security/RESULTATS.md` (lecture des preuves)

## Structure principale

- `backend/`, `frontend/`, `streamer/`, `database/`: composants applicatifs.
- `ingress/`, `loadbalancer/`, `namespace/`, `secret/`: manifests d'infrastructure.
- `security/`: documentation securite, procedures et rapports.

## Positionnement de qualite (niveau ecole d'ingenieur)

- Source de verite declarative: manifests Kubernetes + documentation.
- Tracabilite des actions: preuves horodatees dans `security/reports/`.
- Lisibilite de livraison: nomenclature explicite et documentation en francais.
- Absence de scripts shell custom dans le livrable final.
- Pipeline CI securite explicite et auditable (Gitleaks, KICS).

## Navigation sur la VM

```bash
cd ~/ginflix/security
ls
```

```bash
cd ~/ginflix/security/reports
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```
