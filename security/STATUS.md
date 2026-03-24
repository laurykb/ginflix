# État sécurité / explo — Ginflix

*Référence : 09/03/2026*

## En bref

Manifests durcis, secrets sortis des ConfigMap quand c’était pertinent, politiques Cilium en place, Ingress avec en-têtes de sécurité, CI Gitleaks + KICS. Les preuves sont dans `security/reports/` (voir aussi `reports/INDEX_RESULTATS.md`).

## Ce qui est fait

- Pods : `automountServiceAccountToken: false`, `allowPrivilegeEscalation: false`, `seccompProfile: RuntimeDefault`, `capabilities.drop` là où c’est compatible avec les images.
- Données sensibles : migration vers des `Secret` Kubernetes là où il fallait.
- Réseau : default deny Cilium + règles métier (DNS, ingress front, egress S3 / Keycloak, etc.).
- Ingress : en-têtes type `X-Frame-Options`, `X-Content-Type-Options`, `CSP`, `Permissions-Policy`, `Referrer-Policy`.
- CI : scans **Gitleaks** et **KICS** sur le dépôt.

## Rapports utiles (session VM)

- `security/reports/rapport_iac_trivy_config_20260309_045619/`
- `security/reports/rapport_posture_cluster_20260309_051953/`
- `security/reports/rapport_trivy_secrets_20260309_052025/`
- `security/reports/rapport_kyverno_falco_tentative_1_20260309_061346/`
- `security/reports/rapport_kyverno_falco_tentative_2_20260309_061645/`

## Vérifications HTTP (chemin nominal)

- `/` → 200  
- `/admin` → 200  
- `/api/videos` → 200  

## Kyverno / Falco

Non laissés en prod sur notre Kind : le control-plane a eu des phases où `kube-controller-manager` n’était pas Ready pendant les essais — on documente les tentatives plutôt que de forcer l’outillage.

## Pour la soutenance

On peut expliquer : choix des ressources K8s, réseau, durcissement, limites du lab Kind, et ce qu’il faudrait pour aller plus loin (control-plane stable, admission controller, runtime security).
