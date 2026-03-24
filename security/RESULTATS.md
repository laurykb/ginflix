# Preuves et rapports

Les sorties brutes des outils (json, txt, html) sont rangées par dossier **horodaté** sous `security/reports/`. L’idée : en soutenance, on peut rouvrir exactement ce qui a été exécuté.

## Nommage des dossiers

Exemples utilisés sur le projet :

- `rapport_iac_*` — Trivy sur la config  
- `rapport_posture_*` — vérification de posture cluster  
- `rapport_trivy_secrets_*` — détection de secrets dans les fichiers  
- `rapport_kyverno_falco_*` — essais Kyverno / Falco  
- `rapport_traces_ci_*` — copie d’éléments liés aux workflows GitHub  

Les anciens jeux de résultats sont dans `security/reports/archive/`.

## Ordre de lecture

1. `security/STATUS.md`  
2. `security/reports/INDEX_RESULTATS.md`  
3. Le dossier de rapport qui t’intéresse  
