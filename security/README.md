# Securite GINFLIX

Ce dossier contient les elements securite du projet.

## Objectif

- Appliquer des bonnes pratiques securite sur Kubernetes.
- Conserver des preuves simples a verifier.

## Fichiers importants

- Etat d'avancement: `security/STATUS.md`
- Exploitation des preuves: `security/RESULTATS.md`
- Operations (sans scripts): `security/operations/`
- Rapports techniques: `security/reports/`
- Rapport executif: `security/RAPPORT_SECURITE_VM_20260309.md`

## Outils retenus

- `Trivy`: scan config/secrets.
- `Gitleaks`: detection de secrets en CI.
- `KICS`: analyse IaC/Kubernetes en CI.

Workflows CI actifs:
- `.github/workflows/security-gitleaks.yml`
- `.github/workflows/security-kics.yml`

Configuration associee:
- `.gitleaks.toml`

## Etat actuel

- Hardening workloads applique sur les deploiements critiques.
- Hygiene secrets appliquee (Secret K8s, nettoyage ConfigMap).
- Kyverno/Falco non promus en exploitation a cause d'instabilite control-plane intermittente.

## Regles de lecture

- Lire d'abord `security/STATUS.md`.
- Ensuite `security/reports/INDEX_RESULTATS.md`.
- Les anciens rapports sont dans `security/reports/archive/`.
