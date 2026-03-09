# Securite GINFLIX

Ce dossier regroupe la livraison DevSecOps du projet GINFLIX avec une approche professionnelle, lisible et reproductible.

## Objectif de la livraison

- Proposer un socle securise base sur des manifests Kubernetes explicites.
- Fournir une documentation exploitable en local et sur la VM.
- Conserver des preuves techniques verifiables pour soutenance et audit.

## Navigation

- Etat d'avancement: `security/STATUS.md`
- Exploitation des preuves: `security/RESULTATS.md`
- Operations (sans scripts): `security/operations/`
- Rapports techniques: `security/reports/`
- Rapport executif: `security/RAPPORT_SECURITE_VM_20260309.md`

## Chaine DevSecOps retenue (simple et open source)

- `Trivy` (open source): scans de configuration et secrets, avec preuves deja archivees dans `security/reports/`.
- `Gitleaks` (open source): detection de secrets en CI.
- `KICS` (open source): analyse IaC/Kubernetes en CI.

Workflows CI actifs:
- `.github/workflows/security-gitleaks.yml`
- `.github/workflows/security-kics.yml`

Configuration associee:
- `.gitleaks.toml`

## Ce qui est attendu d'un projet etudiant d'ingenieur

- Architecture claire et minimale.
- Source de verite declarative (manifests + docs), pas de logique cachee.
- Niveau de preuve suffisant: scans techniques et decisions tracees.
- Documentation francaise coherente pour lecteur technique et non auteur du projet.

## Etat actuel (synthese)

- Hardening workloads applique sur les deploiements critiques.
- Hygiene secrets appliquee (Secret K8s, nettoyage ConfigMap).
- Kyverno/Falco non promus en exploitation a cause d'instabilite control-plane intermittente.

## Regles de qualite documentaire

- Commentaires et messages en francais.
- Noms de dossiers/fichiers explicites.
- Chaque tentative importante documentee dans `security/STATUS.md`.
- Rapports bruts conserves dans `security/reports/`.
- Documentation centralisee dans ce fichier pour eviter la dispersion.
