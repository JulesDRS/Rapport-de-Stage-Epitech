@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

Un workflow Git fait généralement référence à l'ensemble des processus et des étapes automatisées qu'un utilisateur ou une équipe suit pour gérer le développement de logiciels au sein d'une plateforme Git.

## Ça sert à quoi ?

Un workflow Gitea permet de structurer et automatiser les processus de développement, de gestion du code, et d'intégration continue (CI). Voici les principales utilisations d'un workflow :

### Gestion des versions et du code :

- Gitea, comme d'autres systèmes basés sur Git, permet aux développeurs de gérer des branches de développement, de fusionner des fonctionnalités, de résoudre des conflits et de gérer des versions de leur code.
- Un workflow typique inclurait la création de branches pour des nouvelles fonctionnalités (feature branches), la fusion (merge) des branches via des pull requests, et la gestion des versions (tags).

### Automatisation des processus :

- Grâce à des pipelines d'intégration continue et de déploiement continu (CI/CD), il est possible de définir des workflows automatisés pour tester, valider et déployer des modifications. Par exemple, chaque fois qu'un développeur soumet une pull request, des tests automatisés peuvent être déclenchés, puis, en cas de succès, une validation peut être faite.
- Les workflows CI/CD dans Gitea peuvent être définis via des fichiers YAML qui décrivent les étapes du processus, comme la compilation, les tests, ou le déploiement.

### Collaboration :

- Les workflows facilitent la collaboration entre les équipes en organisant les contributions des différents membres du projet. Par exemple, un workflow peut spécifier des étapes de revue de code, de vérification des tests avant la fusion, etc.
- Gitea inclut des fonctionnalités pour la revue de code via des pull requests, où les développeurs peuvent commenter, discuter et approuver des modifications avant qu'elles ne soient intégrées au code principal.

### Suivi des bugs et des fonctionnalités :

- Gitea permet aussi de gérer des issues (tickets) pour suivre les bugs, les tâches et les nouvelles fonctionnalités. Un workflow peut inclure des étapes pour l'ouverture d'issues, la discussion autour de celles-ci, et la gestion de leur résolution.

### Exemples de Workflow Git

Un workflow basique pourrait ressembler à ceci :

##### Développement :

- Un développeur crée une nouvelle branche pour une fonctionnalité à partir de la branche principale (master ou main).

##### Test et validation :

- Le code est push sur un dépôt Gitea, ce qui peut automatiquement déclencher des tests (via un système d'intégration continue comme Drone ou Jenkins intégré à Gitea).

##### Revue de code :

- Le développeur soumet une pull request pour intégrer sa branche dans la branche principale. Cette demande de fusion est ensuite révisée par d'autres membres de l'équipe.

##### Fusion :

- Après approbation et validation des tests, la pull request est fusionnée dans la branche principale.

##### Déploiement :

- Optionnellement, le code fusionné peut être automatiquement déployé sur un environnement de production.
