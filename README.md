# wp-package-installator-playbooks
# 📦 wp-package-installator-playbooks

> La bibliothèque d'automatisation pour le plugin **Package Installator**. 
> Déployez des services (Redis, MariaDB, etc.) en "deux deux" via Ansible & Docker.

## 🚀 Concept

Ce dépôt sert de catalogue dynamique pour le plugin WordPress **Package Installator**. 
Il est structuré pour permettre une mise à jour automatique du catalogue sans toucher au code du plugin.

1. **Dossier Service** : Chaque application a son propre dossier dans `playbooks/`.
2. **Auto-Manifest** : Un workflow GitHub Action scanne les dossiers et génère automatiquement le fichier `manifest.json` à la racine.
3. **Déploiement** : Le plugin WordPress clone ce repo et exécute les playbooks via Ansible.

---

## 📂 Structure de la Bibliothèque

Chaque service doit suivre cette structure stricte :

```text
playbooks/
└── [id-du-service]/
    ├── info.json       # Métadonnées (nom, description, options UI)
    └── main.yml        # Playbook Ansible principal
Le fichier info.json
C'est ce fichier qui génère l'interface dans WordPress. Exemple pour un service :

JSON
{
  "id": "redis",
  "name": "Redis Standalone",
  "category": "Database",
  "description": "Instance Redis simple avec persistance.",
  "playbook": "playbooks/redis/main.yml",
  "options": [
    { "key": "redis_port", "label": "Port", "type": "number", "default": 6379 }
  ]
}
🤖 Automatisation (CI/CD)
Ce dépôt utilise GitHub Actions.
À chaque push dans un dossier playbooks/, le fichier manifest.json à la racine est reconstruit automatiquement.

Pourquoi ? Pour que le plugin WordPress n'ait qu'un seul fichier léger à lire pour afficher tout le catalogue.

🤝 Contribuer
Vous voulez ajouter un service (ex: MongoDB, Meilisearch, Nginx) ?

Fork le projet.

Créez un dossier dans playbooks/ avec votre info.json et votre main.yml.

Testez votre playbook en local avec ansible-playbook.

Envoyez une Pull Request.

⚖️ Licence
Ce projet est sous licence The Unlicense. Vous êtes libre de copier, modifier et distribuer ce code sans aucune restriction.
