@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Gitea ?
Gitea est une instance Git OpenSource pouvant être hébergée localement facilement, ce qui accroit la sécurité et la facilité de gestion et de personnalisation. C'est ici que tout notre code va être stocké et manipulé !

## Git ?
Git est un système de contrôle de version décentralisé qui permet aux développeurs de suivre les modifications apportées à un projet, de collaborer sur le code, et de gérer différentes versions de celui-ci. C'est lui qui va manipuler notre code dans l'ombre de Gitea !

<p class="info-note">Et oui, <b>GitHub, GitLab, Gitea</b> ou quelque autre <b>instance Git</b> que ce soit ne sont pas de logiciels propres, dans le sens ou c'est <b>Git qui s'occupe de la manipulation de votre code</b>, toutes ces instances sont juste là pour vous offrir une expérience agréable et fonctionnelle. On peut le comparer à Linux avec ses distributions ou à Androïd avec ses surcouches par exemple</p>

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725287171275.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725287171275.png)

# Installation
<p class="warning-note">La configuration que je vais vous exposer est celle de l'usine logicielle de Symexo et ne vous conviendra peut-être pas, je vous invite quand même à aller faire vos recherche en vous basant sur ce chapitre !</p>

*Pour procéder à cette installation, nous allons nous servir de Portainer installé précédement...*
- Tout d'abord vous allez créer une nouvelle stack, lui donner un nom et coller le code ci-dessous dans l'éditeur de la stack :
```yaml
version: "3"

networks:
  gitea:
    external: false

services:
  server:
    image: gitea/gitea:latest
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
      - GITEA__database__DB_TYPE=mysql
      - GITEA__database__HOST=${HOST}
      - GITEA__database__NAME=${DB_NAME}
      - GITEA__database__USER=${DB_USERNAME}
      - GITEA__database__PASSWD=${DB_PASSWORD}
      - GITEA__server__LOCAL_ROOT_URL=${ROOT_URL}
      - GITEA__server__SSH_DOMAIN=${SSH_DOMAIN}
      - GITEA__server__DOMAIN=${SERVEUR_DOMAIN}
      - GITEA__server__HTTP_PORT=3000
      - GITEA__server__ROOT_URL=${ROOT_URL}
      - GITEA__server__DISABLE_SSH=false
      - GITEA__server__SSH_PORT=${SSH_PORT}
      - GITEA__server__LFS_START_SERVER=true
      - GITEA__server__LFS_JWT_SECRET=${LFS_JWT_SECRET}
      - GITEA__server__OFFLINE_MODE=false
      - GITEA__repository__USE_COMPAT_SSH_URI=true
      - GITEA__repository__DEFAULT_BRANCH=master
      - GITEA__repository__FORCE_PRIVATE=true
      - GITEA__repository__DEFAULT_REPO_UNITS=repo.code,repo.issues,repo.releases,repo.pulls,repo.projects
      - GITEA__attachment__MAX_SIZE=100
      - GITEA__security__INSTALL_LOCK=true
      - GITEA__project__PROJECT_BOARD_BASIC_KANBAN_TYPE=À faire, En recette, En production, Rejeté
      - GITEA__ui__DEFAULT_SHOW_FULL_NAME=true
      - GITEA__mailer__ENABLED=true
      - GITEA__mailer__PROTOCOL=smtp+starttls
      - GITEA__mailer__SMTP_ADDR=${SMT_SERVER}
      - GITEA__mailer__SMTP_PORT=${SMTP_PORT}
      - GITEA__mailer__USER=${USER}
      - GITEA__mailer__PASSWD=${PASSWORD} #(voir keepass)
      - GITEA__mailer__FROM=${MAIL_PROVIDER}
      - GITEA__service__ENABLE_NOTIFY_MAIL=false
      - GITEA__service__SHOW_REGISTRATION_BUTTON=false
      - GITEA__service__ALLOW_ONLY_EXTERNAL_REGISTRATION=true
      - GITEA__service__ENABLE_CAPTCHA=false
      - GITEA__service__DEFAULT_ALLOW_CREATE_ORGANIZATION=false
      - GITEA__service__AUTO_WATCH_NEW_REPOS=false
      - GITEA__picture__DISABLE_GRAVATAR=false
      - GITEA__picture__ENABLE_FEDERATED_AVATAR=true
      - GITEA__openid__ENABLE_OPENID_SIGNIN=false
      - GITEA__openid__ENABLE_OPENID_SIGNUP=false
      - GITEA__log__MODE=file
      - GITEA__log__LEVEL=Error
      - GITEA__indexer_REPO_INDEXER_ENABLED=true
    restart: always
    networks:
      - gitea
    volumes:
      - ./gitea:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"
      - "8443:443"
      - "222:22"
    depends_on:
      - db

  db:
    image: mysql:8
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=gitea
      - MYSQL_USER=gitea
      - MYSQL_PASSWORD=gitea
      - MYSQL_DATABASE=gitea
    networks:
      - gitea
    volumes:
      - ./mysql:/var/lib/mysql
```

<p class="warning-note">Cette configuration est celle de Symexo, vous devrez changer les variables d'environnement</p>
<p class="info-note">Dans ce compose, nous instancions une image et un conteneur Gitea et un sql8 pour stocker les configuration, les dépots et les utilisateur que nous créerons plus tard dans Gitea</p>

- Une fois le code collé vous pouvez cliquer sur le petit bouton bleu **"Deploy the stack"** et le conteneur sera lancé, vous pouvez maintenant aller dans l'onglet "Containers", vous verez votre premier conteneur et sa DB comme ci-dessous :

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725284353584.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725284353584.png)

- Vous allez maintenant vous rendre sur votre Gitea en cliquant sur le lien **"3000:3000"** à droite<br>
Une fois que vous y serez, vérifiez tous les paramètres et appuyez sur le bouton **"Installer"** en bas de la page.<br>
Créez vous un compte et voilà !
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725286331085.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725286331085.png)

<p class="success-note">Vous avez installé et configuré Gitea !</p>

# Mise à jour
Pour ce faire, rien de plus simple ! Si vous avez mis la version "latest", vous pouvez faire comme suit, sinon, changez juste la version et faites la même chose !

- Rendez-vous dans votre stack Gitea, dans **"Editor"**, puis cliquez sur le petit bouton bleu **"Update the stack"** en bas de la section et cochez la case **"Re-pull image and redeploy"** puis validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725285760778.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725285760778.png)

<p class="success-note">Vous venez de mettre à jour Gitea !</p>

# Désinstallation
- Rendez-vous dans l'onglet **"Containers"**, sélectionnez les conteneurs à supprimer (dans notre cas **gitea** et **gitea-db-1**) puis cliquiez sur **"Remove"** en haut à droite, cochez **"Automatically remove non-persistent volumes"** et validez

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725286162078.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725286162078.png)
  
- Allez ensuite dans l'onglet **"Images"** et supprimez les images adéquates, dans notre cas **"gitea/gitea:latest"** et **"mysql:8"**

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725286210250.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725286210250.png)

<p class="info-note">Les networks vides seront automatiquement supprimés</p>
<p class="success-note">Vous venez de désinstaller Gitea de votre système !</p>

# Migration
<p class="warning-note">Cette section est réservée à ceux voulant faire une migration de leurs ancienne instance Gitea à la nouvelle</p>
<p class="info-note">Je vais effectuer toute cette section dans la machine virtuelle hôte du conteneur docker, je vais donc accéder à son volume local (/data/compose/13/ pour ma part) et <b>toute la section se déroulera à l'intérieur</b></p>
<p class="info-note">Pour transférer des données depuis votre système windows à la vm, vous pouvez utiliser un logiciel comme <b>"WinSCP"</b></p>

 **Vous trouverez tous vos chemins dans votre instance Gitea au chemin suivant :<br>
 *Profil et Réglages/administration du site/Configuration/Résumé***
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725289765322.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725289765322.png)

**1) Trouver les fichiers racine et customs de Gitea et les transférer sur la nouvelle instance**

- Vous devrez trouver un dossier contenant tous ces dossiers :
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725288024193.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725288024193.png)

- Vous devrez aussi récupérer, si vous en avez un, le dossier custom, le miens contient ça
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725288088381.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725288088381.png)

  Une fois toutes ces informations récupérées, vous allez **écraser** tout le contenu de **/gitea/gitea/** avec tout ce que vous avez récupérés

**2) Trouver les dépots et les transférer sur la nouvelle instance**

- Vous devez trouver le dossier qui stocke **tous vos dépot** et écraser le contenu de **/gitea/git/repositories/** avec.<br>
  Une fois tout transféré, si vous actualisez votre page Gitea, **les dépots seront importés mais pas leur contenu**, pour celà nous devons aussi **importer la base de données**

**3) Remplacer la DB actuelle par celle de votre ancienne instance Gitea**

- récupérez la sauvegarde de votre base de donnée et placez là dans **/mysql/**
- exécutez la commande suivante pour entrer dans le conteneur :
```bash
docker exec -it $CONTAINER_NAME bash
```
- exécutez la commande suivante pour restaurer votre sauvegarde :
```bash
mysql -u $USERNAME -p $DATABASE_NAME < $BACKUP_FILE
```
Vous trouverez vos identifiants dans la stack gitea, par défaut tout est **"gitea"** <br>
Maintenant, en actualisant la page, le contenu de votre dépo devrait s'afficher !

**4) Importer les clés SSH (Optionnel)**

- Récupérez les clés souhaitées enregistrées sur votre ancienne instance Gitea et importez les dans **/gitea/ssh/** de votre nouvelle instance !

<p class="success-note">Félicitations, vous avez migrer sur une nouvelle instance !</p>

# Installation Gitea Act Runner
<p class="info-note">Le <b>Gitea Act Runner</b> est le composant qui va vous permettre d'<b>exécuter des Workflow Gitea</b>, il est <b>facultatif</b></p>

Ce sera exactement le même processus que pour Gitea, à l'exception que vous devez créer un volume supplémentaire et mettre le compose que je vous donnerai à la place :

- Pour commencer, **rendez-vous sur Portainer pour créer une nouvelle stack contenant le compose suivant**

``` yaml
version: "3.8"
services:
  runner:
    image: gitea/act_runner:latest
    deploy:
      resources:
        limits:
          cpus: "16"
          memory: "32g"
    environment:
      CONFIG_FILE: /config.yaml
      GITEA_INSTANCE_URL: "http://10.2.12.67:3000"
      GITEA_RUNNER_REGISTRATION_TOKEN: "o4sRClHwOGJmglNwmdr921x1puorZa1O3dEPUW1q"
      GITEA_RUNNER_NAME: "PortainerRunner"
      GITEA_RUNNER_TYPE: "instance"
    volumes:
      - ./config.yaml:/config.yaml
      - ./data:/data
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes/m2Directory:/mnt
```
Vous pouvez même rajouter le service au compose de Gitea, mais personnellement j'ai préféré faire une stack à part.

Variables | Description
-|-
$URL_GITEA | l'URL de votre instance Gitea, sous forme d'IP ou d'URL classique
$REGISTRATION_TOKEN_GITEA | Jeton d'enregistrement Gitea
$RUNNER_NAME | Le nom que portera votre runner sur Gitea
$RUNNER_TYPE | Type de runner : default (repository), organization, instance

<p class="warning-note">Ici, j'ai limité l'utilisation CPU et RAM à 16cpus et 32Go, pensez à le changer en fonction de votre système.</p>

- Après ça, vous allez créer le volume: rendez-vous dans l'onglet **"Volumes"** de Portainer et en ajouter un, vous allez le nommer et valider sa création.
- En suite, vous allez vous rendre sur votre terminal et entrer dans le conteneur en tapant la commande suivante :
```bash
docker exec -it ${CONTAINER_NAME_OR_ID} bash
```
- Une fois dans le conteneur, vous allez créer un dossier se nommant **".m2"** puis **rentrer les commandes suivantes**
### création et remplissage du fichier "settings-security_save.xml"
```bash
echo "<settingsSecurity>" > settings-security_save.xml && echo "  <master>{OZDpcR6xKJUHjbLPfTSj2vt13djqMFDMUmPDdWoF+pwLtJn5ub4lN/mf15yTW7ZW}</master>" >> settings-security_save.xml && echo "</settingsSecurity>" >> settings-security_save.xml
```
### création et remplissage du fichier "setting_save.xml"
```bash
echo "<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"" > settings_save.xml  && echo "  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"" >> settings_save.xml  && echo "  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">" >> settings_save.xml  && echo "  <servers>" >> settings_save.xml  && echo "    <server>" >> settings_save.xml  && echo "      <id>${SETTINGS_RELEASE_ID}</id>" >> settings_save.xml  && echo "      <username>${USERNAME}</username>" >> settings_save.xml  && echo "      <password>${PASSWORD}</password>" >> settings_save.xml  && echo "    </server>" >> settings_save.xml  && echo "    <server>" >> settings_save.xml  && echo "      <id>${SETTINGS_SNAPSHOTS_ID}</id>" >> settings_save.xml  && echo "      <username>${USERNAME}</username>" >> settings_save.xml  && echo "      <password>${PASSWORD}</password>" >> settings_save.xml  && echo "    </server>" >> settings_save.xml  && echo "  </servers>" >> settings_save.xml  && echo "  <profiles>" >> settings_save.xml  && echo "    <profile>" >> settings_save.xml  && echo "                <id>repository.symexo</id>" >> settings_save.xml  && echo "                <activation>" >> settings_save.xml  && echo "                        <activeByDefault>true</activeByDefault>" >> settings_save.xml  && echo "                </activation>" >> settings_save.xml  && echo "                <repositories>" >> settings_save.xml  && echo "                        <repository>" >> settings_save.xml  && echo "                                <id>nexus_releases</id>" >> settings_save.xml  && echo "                                <name>Symexo Release</name>" >> settings_save.xml  && echo "                                <releases>" >> settings_save.xml  && echo "                                        <enabled>true</enabled>" >> settings_save.xml  && echo "                                </releases>" >> settings_save.xml  && echo "                                <snapshots>" >> settings_save.xml  && echo "                                        <enabled>false</enabled>" >> settings_save.xml  && echo "                                </snapshots>" >> settings_save.xml  && echo "                                <url>${YOUR_RELEASE_REPO}</url>" >> settings_save.xml  && echo "                        </repository>" >> settings_save.xml  && echo "                        <repository>" >> settings_save.xml  && echo "                                <id>nexus_snapshots</id>" >> settings_save.xml  && echo "                                <name>Symexo Snapshots</name>" >> settings_save.xml  && echo "                                <releases>" >> settings_save.xml  && echo "                                        <enabled>false</enabled>" >> settings_save.xml  && echo "                                </releases>" >> settings_save.xml  && echo "                                <snapshots>" >> settings_save.xml  && echo "                                        <enabled>true</enabled>" >> settings_save.xml  && echo "                                </snapshots>" >> settings_save.xml  && echo "                                <url>${YOUR_SNAPSHOTS_REPO}</url>" >> settings_save.xml  && echo "                        </repository>" >> settings_save.xml  && echo "                        <repository>" >> settings_save.xml  && echo "                                <id>java-moovapps-public</id>" >> settings_save.xml  && echo "                                <url>https://repository.devops.moovapps.com/repository/java-moovapps-public/</url>" >> settings_save.xml  && echo "                                <releases>" >> settings_save.xml  && echo "                                        <enabled>true</enabled>" >> settings_save.xml  && echo "                                </releases>" >> settings_save.xml  && echo "                                <snapshots>" >> settings_save.xml  && echo "                                        <enabled>false</enabled>" >> settings_save.xml  && echo "                                </snapshots>" >> settings_save.xml  && echo "                        </repository>" >> settings_save.xml  && echo "                </repositories>" >> settings_save.xml  && echo "        </profile>" >> settings_save.xml  && echo "  </profiles>" >> settings_save.xml  && echo "</settings>" >> settings_save.xml
```
- Maintenant que vous avez faits tout ça, vous allez sortir du container en tapant la commande ```exit```.

## Comment récupérer le Jeton d'enregistrement Gitea
<p class="info-note">Ici nous allons configurer une Runner en Global (instance)</p>

- Rendez-vous dans ***Profil et Réglages/Configuration/Actions/Exécuteurs*** ou au chemin suivant ***https://gitea_example.com/user/settings/actions/runners***.
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725354419874.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725354419874.png)
- Une fois dans ce menu, vous allez cliquer sur le bouton bleu e haut à droite **"Créer un nouvel exécuteur"** puis copiez le **REGISTRATION TOKEN**.
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725354511707.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725354511707.png)

<p class="info-note">Pour plus d'informations, vous pouvez directement aller sur la doc Gitea pour la configuration</p>
<p class="success-note">Vous avez installer et configurer un <b>Gitea Action Runner</b> !</p>