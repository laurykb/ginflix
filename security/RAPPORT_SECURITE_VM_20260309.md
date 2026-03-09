# Rapport de securisation Kubernetes - GINFLIX (VM)

Date: 09/03/2026  
Perimetre: cluster Kubernetes GINFLIX sur VM (`~/ginflix`)  
Objectif: fournir une trace presentable des changements, ameliorations, tests et resultats.

## 1) Resume executif

- La demarche a ete basculee en mode `manifest-first` et `documentation-first`.
- Les durcissements workloads et hygiene secrets sont en place et appliques sur la VM.
- Les controles OWASP applicables immediatement ont ete executes avec preuves:
  - scan IaC/manifests
  - verification posture cluster
  - secrets detection
- Disponibilite applicative preservee en sortie de travaux (`/`, `/admin`, `/api/videos` en `200` via le chemin HTTP de contournement).

## 2) Ce qui a change (trace de configuration)

### Documentation et gouvernance

- `security/README.md`
  - formalisation de la source de verite: manifests + docs
  - scripts shell repositionnes comme outillage operationnel optionnel
- `security/STATUS.md`
  - matrice OWASP priorisee
  - execution reelle sur VM (preuves, resultats, points restants)

### Manifests Kubernetes durcis

- `backend/app/backend-deployment.yaml`
- `frontend/frontend-user/app/frontend-deployment.yaml`
- `frontend/frontend-admin/app/frontend-admin-deployment.yaml`
- `streamer/app/streamer-deployment.yaml`

Ameliorations appliquees:
- `automountServiceAccountToken: false`
- `seccompProfile: RuntimeDefault`
- `allowPrivilegeEscalation: false`
- `capabilities.drop: [ALL]` la ou compatible
- consommation des secrets via `Secret` (et non ConfigMap pour les valeurs sensibles)

## 3) Tests et scans executes (avec preuves)

### 3.1 Scan IaC/manifests (OWASP - misconfiguration)

- Rapport: `security/reports/20260309_045619/trivy-config.json`
- Synthese: `HIGH_CRITICAL_COUNT=22`

### 3.2 Verification posture cluster

- Rapport de reference: `security/reports/20260309_051953/verify-cluster-security.txt`
- Resultat: `Summary: 28 pass, 0 fail`

### 3.3 Secrets detection

- Rapport: `security/reports/20260309_052025/trivy-secrets.json`
- Resultat: `SECRETS_FOUND=0`


## 4) Disponibilite service (preuve fonctionnelle)

Verification externe (HTTP workaround):
- `/` -> `200`
- `/admin` -> `200`
- `/api/videos` -> `200`

## 5) Risques residuels et plan de remediation

### Priorite 1 - Stabilite infra

Objectif: maintenir une disponibilite stable du cluster et des services.

Actions:
- conserver la surveillance du control-plane
- valider systematiquement les chemins applicatifs critiques

### Priorite 2 - Pod Security restricted complet

Objectif: reduire les warnings PSS.

Actions:
- tester `runAsNonRoot` et ajuster images front/back si necessaire
- evaluer `capabilities.drop: [ALL]` pour frontends sans casser Nginx
- valider par rollout + smoke tests + verify script.

### Priorite 3 - Admission et runtime controles avances

Objectif: finaliser Kyverno/Falco sans destabiliser le cluster.

Actions:
- conserver les prechecks de stabilite control-plane
- deploiement seulement sur fenetre stable continue
- commencer en mode audit/observation.

## 6) Capacite de presentation

Ce rapport est exploitable en soutenance/projet car il relie:
- les changements techniques (fichiers modifies),
- les preuves de verification (rapports horodates),
- les resultats de securite quantifies,
- et le plan de remediation restant.
