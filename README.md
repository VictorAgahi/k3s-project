# K3s GitOps Cluster

## Introduction
Ce projet est un framework de déploiement GitOps utilisant **K3s** pour l'hébergement d'applications modernisées avec une infrastructure résiliente et auto-scalée.

### Stack Technique
*   **Cluster** : K3s
*   **GitOps** : ArgoCD
*   **Ingress** : Traefik & Cloudflare Tunnels (optionnel)
*   **Certificats** : Cert-manager (Let's Encrypt)
*   **Secrets** : Sealed Secrets (Bitnami)
*   **Monitoring** : Kube-Prometheus-Stack, Alloy, Loki, Tempo

---

## Structure du projet

```bash
k3s-project/
├── apps/           # Vos applications (Deployments, Services, Ingress)
├── infra/          # Infrastructure de base (Traefik, Cert-manager, etc.)
├── meta/           # Définitions ArgoCD pour l'orchestration
├── argocd/         # Configuration et bootstrap d'ArgoCD
├── monitoring/     # Configuration de la stack d'observabilité
├── valueFiles/     # Helm values pour les composants infra
└── setup.sh        # Script d'installation initial
```

---

## Installation

1.  **Prérequis** : Un serveur Linux (Ubuntu recommandé) avec un accès SSH.
2.  **Configuration** : Modifiez les variables dans `setup.sh` (Tokens Cloudflare, etc.).
3.  **Lancement** :
    ```bash
    chmod +x setup.sh
    ./setup.sh
    ```

---

## Déployer une nouvelle application

1.  Créez un dossier dans `apps/mon-app/` avec vos manifestes Kubernetes.
2.  Créez un fichier dans `meta/apps-mon-app.yaml` en vous inspirant des modèles existants.
3.  Poussez vos changements sur la branche `main`. ArgoCD détectera automatiquement la nouvelle application.

---

## Maintenance & Monitoring
Une fois installé, accédez à l'interface d'ArgoCD sur le port configuré pendant le setup pour suivre l'état de vos déploiements.
La stack de monitoring (Grafana/Loki) est accessible via les Ingress configurés dans `monitoring/`.