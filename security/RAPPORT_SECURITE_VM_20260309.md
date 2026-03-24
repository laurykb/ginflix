# Rapport sécurité — Ginflix (VM)

**Date :** 09/03/2026  
**Périmètre :** cluster Kind / manifests déployés sur la VM (`~/ginflix`).

## Synthèse

On a surtout travaillé les **manifests** : durcissement des pods, secrets dans des `Secret` plutôt que dans des ConfigMap pour ce qui est sensible, Cilium, en-têtes sur l’Ingress. Les scans (Trivy config, Trivy secrets, script de posture) sont archivés dans `security/reports/` avec la date dans le nom du dossier. À la fin des modifs, les URLs testées en HTTP donnaient toujours du **200** sur `/`, `/admin` et `/api/videos`.

## Fichiers Kubernetes modifiés (durcissement)

- `backend/app/backend-deployment.yaml`
- `frontend/frontend-user/app/frontend-deployment.yaml`
- `frontend/frontend-admin/app/frontend-admin-deployment.yaml`
- `streamer/app/streamer-deployment.yaml`

Réglages typiques : `automountServiceAccountToken: false`, `seccompProfile: RuntimeDefault`, `allowPrivilegeEscalation: false`, `capabilities.drop: [ALL]` quand l’image le permet.

## Preuves (où les retrouver)

| Contrôle | Dossier / fichier |
|----------|-------------------|
| Trivy config (IaC) | `security/reports/rapport_iac_trivy_config_20260309_045619/` — à l’époque synthèse notée : `HIGH_CRITICAL_COUNT=22` |
| Posture cluster | `security/reports/rapport_posture_cluster_20260309_051953/verify-cluster-security.txt` — `28 pass, 0 fail` |
| Secrets dans les fichiers | `security/reports/rapport_trivy_secrets_20260309_052025/` — `SECRETS_FOUND=0` |

*(Les chemins `security/reports/20260309_*` sans préfixe `rapport_…` dans une ancienne version de ce rapport étaient incorrects.)*

## HTTP (smoke)

- `/` → 200  
- `/admin` → 200  
- `/api/videos` → 200  

## Reste à faire si on prolonge le projet

- Surveiller le **control-plane** sur Kind avant de réessayer Kyverno / Falco (voir dossiers `rapport_kyverno_falco_tentative_*`).
- Pousser plus loin **Pod Security** (`runAsNonRoot`, etc.) en testant bien les images nginx / binaires fournis.
- Enchaîner admission / runtime seulement quand le cluster tient stable plusieurs heures d’affilée.

La doc à jour du volet sécurité est dans `security/README.md` et `security/STATUS.md`.
