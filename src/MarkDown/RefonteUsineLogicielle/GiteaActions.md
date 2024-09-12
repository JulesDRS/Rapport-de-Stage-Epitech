@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

Gitea Actions est un système d'intégration continue (CI) et d'automatisation des tâches, similaire à GitHub Actions, mais spécifiquement conçu pour le logiciel Gitea.

![alt text](../../assets/images/Gitea/Actions/DevOps.png)

## Ça sert à quoi ?

Les Gitea Actions permettent d'exécuter des scripts ou des commandes automatiquement en réponse à des événements spécifiques, tels que les commits, les pull requests ou encore à des moments définis. En bref, c'est un mécanisme d'automatisation du développement et de déploiement.

Les Gitea Actions sont particulièrement utiles pour :

### Intégration continue (CI) et déploiement continu (CD) :

- Exécuter des tests unitaires à chaque nouveau commit.
- Lancer des builds automatiques du projet après chaque push ou pull request.
- Déployer automatiquement une application après un build réussi, sur un serveur de production ou de staging.

### Automatisation des tâches récurrentes :

- Lancer des scripts de maintenance.
- Nettoyer ou optimiser des ressources régulièrement (par exemple, supprimer des fichiers temporaires ou archiver d'anciens logs).
- Exécuter des scripts de migration ou de gestion de base de données.

### Contrôle de qualité :

- Vérifier la qualité du code avec des outils comme SonarQube ou analyseurs statiques.
- S'assurer que les normes de codage ou les conventions sont respectées automatiquement.

### Automatisation des workflows collaboratifs :

- Mettre à jour automatiquement les versions ou les changelogs à chaque nouvelle version publiée.
- Répondre automatiquement à certains types de pull requests ou issues.

## Comment ça marche ?

Les Gitea Actions fonctionnent à travers des fichiers de configuration définis dans le projet (souvent au format YAML), similaires aux workflows des GitHub Actions. Voici les étapes générales pour utiliser les Gitea Actions :

- Créer un fichier de workflow : Vous définissez les actions que vous souhaitez automatiser dans un fichier, par exemple .gitea/workflows/workflow.yml.
- Définir des déclencheurs (events) : Vous spécifiez des événements qui déclenchent les actions, comme un push, une pull_request ou une release.
- Définir des étapes (jobs) : Chaque étape exécute une série de commandes ou de scripts.
- Exécuter les actions : Les workflows sont exécutés automatiquement lorsqu'ils sont déclenchés par l'événement défini.

## Pourquoi c'est cool ?

- Auto-hébergement : Comme Gitea, les Gitea Actions peuvent être auto-hébergées, ce qui donne un contrôle total sur votre infrastructure, contrairement à des solutions SaaS comme GitHub.
- Léger : Gitea est réputé pour sa légèreté et sa rapidité, ce qui en fait une bonne option pour les petits projets ou les équipes qui cherchent une solution Git simple.
- Flexibilité : Les actions permettent d'automatiser pratiquement n'importe quelle tâche liée à votre projet, rendant les workflows plus efficaces.
