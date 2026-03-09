# Operations securite (sans scripts)

Ce dossier regroupe les commandes d'exploitation sous forme de procedures Markdown.
Objectif: un livrable lisible, auditable et reproductible sans scripts bash custom.

## Fichiers

- `COMMANDES_VM.md`: commandes de verification et d'exploitation sur la VM.
- `TENTATIVE_KYVERNO_FALCO.md`: protocole de tentative et diagnostic associe.

## Principe

- Pas de scripts shell versionnes.
- Les actions se font via manifests Kubernetes et commandes explicites documentees.
- Toute execution importante doit etre tracee dans `security/STATUS.md` et `security/reports/`.
