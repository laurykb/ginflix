# Kyverno / Falco — ce qu’on a essayé

On voulait voir si on pouvait ajouter un minimum de Kyverno + Falco sans faire tomber Ginflix.

## Avant de lancer quoi que ce soit

- Les 3 nœuds en `Ready`
- `kube-controller-manager` et `kube-scheduler` en `Ready`
- Curl OK sur `/`, `/admin`, `/api/videos`

## Déroulé (à la main, pas de script)

1. `helm repo update`
2. Install Kyverno léger
3. Regarder les pods `kyverno` + webhooks
4. Install Falco léger
5. Pods / DaemonSet dans `falco`
6. Retester l’app
7. Garder les logs et `kubectl get` dans `security/reports/`

## Bilan au 09/03/2026

Installations instables sur notre Kind : le control-plane lâchait par moments (`kube-controller-manager` plus Ready). Plutôt que bricoler en boucle la veille de la soutenance, on a documenté les essais et laissé Kyverno/Falco de côté pour ce rendu.
