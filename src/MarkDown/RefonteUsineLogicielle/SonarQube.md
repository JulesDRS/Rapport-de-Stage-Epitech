@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## SonarQube ?
SonarQube est une plateforme open-source de **gestion de la qualité du code**.

## Et ça sert à quoi ?
Elle est utilisée pour **inspecter en continu le code source** des applications, **détecter les défauts**, et **assurer le respect des bonnes pratiques de développement**. SonarQube **analyse le code** pour identifier divers types de problèmes, tels que **les bugs**, **les vulnérabilités de sécurité**, **les "code smells"** (mauvaises pratiques de programmation) et **les problèmes de complexité du code**.

# Installation
*Pour procéder à cette installation, nous allons nous servir de Portainer installé précédement...*
- Tout d'abord vous allez créer une nouvelle stack, lui donner un nom et coller le code ci-dessous dans l'éditeur de la stack :
```yaml
version: "3"

services:
  sonarqube:
    image: sonarqube:community
    depends_on:
      - db
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://db:5432/sonar
      SONAR_JDBC_USERNAME: sonar
      SONAR_JDBC_PASSWORD: sonar
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_logs:/opt/sonarqube/logs
    ports:
      - "5000:9000"
  db:
    image: postgres:12
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: sonar
    volumes:
      - postgresql:/var/lib/postgresql
      - postgresql_data:/var/lib/postgresql/data


volumes:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:
  postgresql:
  postgresql_data:
```

<p class="info-note">Dans ce compose, nous instancions une image et un conteneur SonarQube et un Postgres12 pour stocker les utilisateur et le code que nous y enverrons</p>

- Une fois le code collé vous pouvez cliquer sur le petit bouton bleu **"Deploy the stack"** et le conteneur sera lancé, vous pouvez maintenant aller dans l'onglet "Containers", vous verez votre conteneur SonarQube
- Vous pouvez maintenant vous rendre sur votre SonarQube en cliquant sur le lien **"5000:9000"** à droite et vous créer un compte

<p class="success-note">Vous avez installer <b>SonarQube</b> !</p>

# Mise à jour
Pour ce faire, rien de plus simple ! Si vous avez mis la version "latest", vous pouvez faire comme suit, sinon, changez juste la version et faites la même chose !

- Rendez-vous dans votre stack Gitea, dans **"Editor"**, puis cliquez sur le petit bouton bleu **"Update the stack"** en bas de la section et cochez la case **"Re-pull image and redeploy"** puis validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725285760778.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725285760778.png)

<p class="success-note">Vous venez de mettre à jour <b>SonarQube</b> !</p>

# Désinstallation
- Rendez-vous dans l'onglet **"Containers"**, sélectionnez les conteneurs à supprimer (dans notre cas **sonarqube-sonarqube-1** et **sonarqube-db-1**) puis cliquiez sur **"Remove"** en haut à droite, cochez **"Automatically remove non-persistent volumes"** et validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725356267594.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725356267594.png)
- Allez ensuite dans l'onglet **"Images"** et supprimez les images adéquates, dans notre cas **"sonarqube:community"** et **"postgres:12"**
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725356325239.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725356325239.png)
  
<p class="info-note">Les networks vides seront automatiquement supprimés</p>
<p class="success-note">Vous venez de désinstaller <b>SonarQube</b> de votre système !</p>