# Sécurité — Ginflix

Documentation et **preuves** (captures de commandes, sorties d’outils) produites pendant le projet.

## Où regarder

| Fichier / dossier | Contenu |
|-------------------|---------|
| `security/STATUS.md` | Synthèse : ce qui est en place, ce qui bloque, liens vers les rapports |
| `security/RESULTATS.md` | Comment lire les dossiers de preuves |
| `security/operations/` | Notes d’essais (ex. Kyverno / Falco) |
| `security/reports/` | Rapports horodatés + `INDEX_RESULTATS.md` |
| `security/RAPPORT_SECURITE_VM_20260309.md` | Rapport récap sur la VM (session du 09/03/2026) |

## Outils

- **Trivy** — config / secrets sur les manifests  
- **Gitleaks** — CI, fuites de secrets dans le dépôt  
- **KICS** — CI, analyse IaC Kubernetes  

Workflows : `.github/workflows/security-gitleaks.yml`, `security-kics.yml` — config Gitleaks : `.gitleaks.toml`.

## Point d’attention

Kyverno et Falco ont été **testés** mais **non gardés** en exploitation sur notre cluster : instabilités côté control-plane (détails dans `STATUS.md`). Le reste (durcissement des pods, secrets, Cilium, headers Ingress, CI) reste la base défendable en soutenance.
