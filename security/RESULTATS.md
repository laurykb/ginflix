# Resultats et preuves

Ce document centralise la lecture des preuves techniques produites pendant le projet.

## Regles de lisibilite

- Un dossier de rapport = une execution importante.
- Noms explicites et horodates obligatoires.
- Fichiers bruts conserves (json/html/txt).
- Resume d'analyse present dans `security/STATUS.md`.

## Nommage recommande

- `rapport_iac_<YYYYMMDD_HHMMSS>/`
- `rapport_posture_<YYYYMMDD_HHMMSS>/`
- `rapport_kyverno_falco_<YYYYMMDD_HHMMSS>/`
- `rapport_traces_ci_<YYYYMMDD_HHMMSS>/`

## Lecture rapide

1. Lire `security/STATUS.md`.
2. Ouvrir `security/reports/INDEX_RESULTATS.md`.
3. Consulter le dossier de rapport vise.

## Exemple de preuves de reference (session 09/03/2026)

- Verification posture cluster.
- Scans Trivy config + secrets.
- Traces CI (workflows, checksums, inventaire).
- Tentatives Kyverno/Falco avec causes d'echec tracees.
