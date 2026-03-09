# Tentative Kyverno / Falco

## Objectif

Valider si l'installation minimale de Kyverno et Falco est possible sans degrader la disponibilite.

## Prechecks obligatoires

- 3 noeuds `Ready`
- `kube-controller-manager` `Ready`
- `kube-scheduler` `Ready`
- Application `200` sur `/`, `/admin`, `/api/videos`

## Procedure manuelle (resume)

1. Mettre a jour les repos Helm.
2. Tenter Kyverno minimal.
3. Verifier pods namespace `kyverno` + webhooks.
4. Tenter Falco minimal.
5. Verifier pods/daemonset namespace `falco`.
6. Verifier impact applicatif.
7. Archiver les sorties dans `security/reports/`.

## Etat actuel (09/03/2026)

- Tentatives executees, installations non stabilisees.
- Cause dominante: instabilite intermittente du control-plane (`kube-controller-manager` non Ready pendant la fenetre).
- Decision: conserver Kyverno/Falco en `NEXT`, sans forcer en production etudiante tant que la stabilite infra n'est pas durable.
