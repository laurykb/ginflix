# Rapports (`security/reports/`)

Sorties d’outils et captures de commandes, **une session = un dossier** avec date/heure dans le nom.

- Rapports encore utiles pour la soutenance : préfixe `rapport_*` à la racine de ce dossier.
- Anciens jeux : `archive/`.
- Index manuel possible : `INDEX_RESULTATS.md`.

Lister les dossiers (sans script dédié) :

```bash
cd security/reports
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```

Pour les archives :

```bash
cd security/reports/archive
find . -mindepth 1 -maxdepth 1 -type d | sort -r
```
