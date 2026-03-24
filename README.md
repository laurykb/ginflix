# Ginflix

Dépôt des manifests Kubernetes pour **Ginflix** : mini plateforme de streaming VOD déployée sur un cluster **Kind** (Kubernetes in Docker), dans le cadre d’un projet DevOps.

---

## Contexte du projet

Le travail consiste à se placer en **ingénieur DevOps** : le code applicatif et les images de conteneurs sont fournis (registry interne à Télécom) ; **votre livrable**, c’est le déploiement sur Kubernetes : choix et configuration des ressources (Deployments, Services, Namespace, Ingress, politiques réseau, réplicas, probes, etc.).

Deux briques **hors cluster Kind** sont déjà assurées par d’autres équipes : vous n’avez pas à les déployer, seulement à **y connecter** l’application (endpoints, identifiants, secrets).

---

## Description fonctionnelle

### Utilisateur (site principal)

Un utilisateur accède au site Ginflix (ex. `https://ginflix.gin-telecom.ovh`) et est servi par le **frontend**.

- **Frontend** : pod **nginx** qui sert la page web (`index.html` + JavaScript). Le JS dialogue avec le **backend** (catalogue, métadonnées) et avec le **streamer** quand l’utilisateur lance une lecture.

- **Backend** : API **gRPC** consommée par le frontend. Elle expose notamment les contenus disponibles en s’appuyant sur la **base de données**. Les miniatures des vidéos sont lues depuis un **stockage type S3** (API compatible AWS S3), **en dehors** du cluster Kind (datacenter).

- **Database** : **MongoDB** qui stocke la liste / métadonnées des contenus.

- **Streamer** : pod **nginx** qui sert le flux vidéo au format **HLS**. Les segments sont récupérés via l’API S3 depuis le même type de stockage externe.

### Administration

L’administrateur utilise une **URL distincte** (ex. `https://admin.ginflix.gin-telecom.ovh`) et est servi par **frontend-admin** (nginx + JS), avec parcours d’authentification **Keycloak** (IAM) : redirection éventuelle, puis **JWT** en cas de succès. Le JS admin appelle une **API gRPC d’administration** sur le backend ; le backend valide le token auprès de l’IAM. Cette API permet d’ajouter des vidéos : transcodage **HLS** via **FFmpeg**, envoi des segments et d’une miniature vers le bucket S3, puis création d’une entrée en base. Une fois en ligne, la lecture peut être testée (y compris via le streamer).

> Les noms de domaine ci-dessus sont **exemples** issus de l’énoncé ; à adapter à votre environnement et à votre Ingress.

---

## Services externes (rappel)

| Service | Rôle |
|--------|------|
| **S3 (Garage)** | Stockage objet compatible API S3 ; un bucket par groupe. |
| **IAM (Keycloak)** | Authentification ; dans le cadre du projet, seule l’**interface d’administration** est protégée de cette façon. |

---

## Périmètre Kubernetes (votre travail)

Vous concentrez le déploiement sur **cinq** composants :

1. **frontend**  
2. **frontend-admin**  
3. **backend**  
4. **streamer**  
5. **database** (MongoDB)

---

## Cahier des charges (extraits)

- **Database** : service **interne au cluster** — **pas** d’exposition depuis l’extérieur du cluster.
- **Streamer, frontend, frontend-admin, backend** : accessibles depuis un **navigateur sur le réseau Télécom Paris** (démo devant les enseignants).
- **Fiabilité** : anticiper la panne d’un nœud ; le service doit rester disponible avec une interruption **minimale** et **sans intervention manuelle** (réplication, scheduling, probes, etc. — à argumenter dans vos choix).
- **Sécurité** : à traiter sérieusement (durcissement des pods, secrets, segmentation réseau, headers côté Ingress, scans IaC / secrets en CI, etc.).

---

## Arborescence du dépôt

| Dossier / fichier | Rôle |
|-------------------|------|
| `namespace/` | Namespace et ressources de base |
| `backend/`, `frontend/`, `streamer/`, `database/` | Manifests des composants applicatifs |
| `ingress/`, `loadbalancer/`, `service-nodeport/` | Exposition HTTP / accès depuis le réseau |
| `CiliumNetworkPolicies/` | Politiques réseau (segmentation) |
| `metrics-server/` | Prérequis pour le HPA si utilisé |
| `secret/` | **Exemples** de secrets — ne pas réutiliser tels quels en production |
| `security/` | Notes d’état, rapports et preuves (scans, posture) |
| `config-map-ginflix.yaml` | ConfigMap principale applicative |
| `kind-cilium.yaml` | Cluster Kind avec Cilium |

## CI sécurité (GitHub Actions)

- `.github/workflows/security-gitleaks.yml` — détection de secrets  
- `.github/workflows/security-kics.yml` — analyse IaC / Kubernetes  

Configuration Gitleaks : `.gitleaks.toml`

## Lecture complémentaire (sécurité)

1. [`security/README.md`](security/README.md)  
2. [`security/STATUS.md`](security/STATUS.md)  
3. [`security/RESULTATS.md`](security/RESULTATS.md)  

Outils utilisés côté analyse : **Trivy**, **Gitleaks**, **KICS** (voir détails dans `security/`).
