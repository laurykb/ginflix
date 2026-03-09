# Dossier des rapports

Ce dossier contient les preuves techniques produites pendant les analyses de securite.

## Structure recommandee

- `rapport_*`: rapports actifs utilises pour la soutenance.
- `rapport_traces_ci_*`: preuves CI (workflows, checksums, inventaire).
- `archive/`: anciens rapports conserves pour audit, hors lecture prioritaire.

## Regle de lisibilite

Chaque execution doit produire un dossier de resultat explicite avec:

- date/heure dans le nom du dossier
- fichiers bruts (json/html/txt)
- un fichier d'index lisible (`INDEX_RESULTATS.txt`)

## Exemples de rapports

- Trivy config / secrets
- Traces CI (Gitleaks / KICS)
- Verification posture cluster
- Tentatives Kyverno / Falco

## Generation d'un index global

Commande recommandee (sans script):

```bash
cd security/reports
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```

Commande pour les archives:

```bash
cd security/reports/archive
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```

Le fichier `security/reports/INDEX_RESULTATS.md` peut etre maintenu manuellement pour la soutenance.
