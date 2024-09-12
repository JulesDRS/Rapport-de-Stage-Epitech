@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Diun ?
Diun (Docker Image Update Notifier) est un outil open-source qui **surveille les images Docker pour détecter les nouvelles versions et notifier les utilisateurs lorsqu'une mise à jour est disponible**. C'est particulièrement utile pour les environnements où plusieurs conteneurs Docker sont utilisés, car il permet de maintenir les images à jour, améliorant ainsi la sécurité et la stabilité des services.

# Installation
<p class="warning-note">La configuration que je vais vous fournir est celle de Symexo, il y a par exemple d'autre types de notification, je vous invite à aller, si vous le souhaitez, faier vos recherches...</p>

*Pour procéder à cette installation, nous allons nous servir de Portainer installé précédement...*
- Tout d'abord vous allez créer une nouvelle stack, lui donner un nom et coller le code ci-dessous dans l'éditeur de la stack :
```yaml
version: "3.5"

services:
  diun:
    image: crazymax/diun:latest
    restart: unless-stopped
    command: serve
    volumes:
      - "./data:/data"
      - "/var/run/docker.sock:/var/run/docker.sock"
    environment:
      - "TZ=Europe/Paris"
      - "LOG_LEVEL=info"
      - "LOG_JSON=false"
      - "DIUN_WATCH_WORKERS=20"
      - "DIUN_WATCH_SCHEDULE=0 */6 * * *"
      - "DIUN_WATCH_JITTER=30s"
      - "DIUN_PROVIDERS_DOCKER=true"
      - "DIUN_PROVIDERS_DOCKER_WATCHBYDEFAULT=true"
      - "DIUN_NOTIF_MAIL_FROM=$MAIL_SOURCE"
      - "DIUN_NOTIF_MAIL_TO=$MAIL_DESTINATOR"
      - "DIUN_NOTIF_MAIL_HOST=$YOUR_MAIL_HOST"
      - "DIUN_NOTIF_MAIL_PORT=$YOUR_PORT"
      - "DIUN_NOTIF_MAIL_USERNAME=$YOUR_USERNAME"
      - "DIUN_NOTIF_MAIL_PASSWORD=$YOUR_PASSWORD"
```
<p class="info-note">Dans ce compose, nous instancions une image et un conteneur <b>Carzymax Diun</b> et parametrons toutes les variables nécessaire pour notre configuration</p>

Variables | Description
-|-
TZ | TimeZone ou Fuseau Horaire en français de votre localisation
LOG_LEVEL | Niveau d'information donné dans les notifications
LOG_JSON | Format des Logs : false (Tout public), true (Adapté pour le parsing)
DIUN_WATCH_WORKERS | nombre d'instance de vérification
DIUN_WATCH_SCHEDULE | fréquence à laquelle Diun va vérifier la disponibilité de nouvelles versions des images Docker
DIUN_WATCH_JITTER | Période de jitter, légère variation aléatoire de 0 à 30s ici ajoutée au moment où Diun exécute la tâche de surveillance
DIUN_PROVIDERS_DOCKER | Active ou non le fournisseur Docker dans Diun. Cela signifie que Diun va surveiller les conteneurs Docker sur l'hôte où il est exécuté pour vérifier les mises à jour des images associées.
DIUN_PROVIDERS_DOCKER_WATCHBYDEFAULT | S'il est à true il surveille tous les conteneurs sauf ceux qui sont explicitement exclus
DIUN_NOTIF_MAIL_FROM | Définit l'adresse email de l'expéditeur pour les notifications envoyées par Diun
DIUN_NOTIF_MAIL_TO | Définit l'adresse email du destinataire qui recevra les notifications de mise à jour des images Docker
DIUN_NOTIF_MAIL_HOST | Spécifie le serveur SMTP qui sera utilisé pour envoyer les emails
DIUN_NOTIF_MAIL_PORT | Définit le port utilisé pour se connecter au serveur SMTP (par exemple, 587 pour TLS)
DIUN_NOTIF_MAIL_USERNAME | Le nom d'utilisateur pour l'authentification auprès du serveur SMTP
DIUN_NOTIF_MAIL_PASSWORD | Le mot de passe pour l'authentification auprès du serveur SMTP

- Une fois le code collé vous pouvez cliquer sur le petit bouton bleu **"Deploy the stack"** et le conteneur sera lancé, vous pouvez maintenant aller dans l'onglet "Containers", vous verez votre contreneur **Diun**:
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725371674708.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725371674708.png)

Maintenant, Diun surveillera tous vos conteneurs et vous enverra des notification lors de mises à jour disponible. Pour tester les notifications vous pouvez directement exécuter les commandes suivantes dans le terminal hôte du conteneur docker
```bash
docker exec diun-diun-1 diun notif test
```
Remplacez **"diun-diun-1"** par le nom de votre conteneur ou son ID.

<p class="success-note"> Et voilà, vous avez installé Diun !</p>`

# Mise à jour
Pour ce faire, rien de plus simple ! Si vous avez mis la version "latest", vous pouvez faire comme suit, sinon, changez juste la version et faites la même chose !

- Rendez-vous dans votre stack Diun, dans **"Editor"**, puis cliquez sur le petit bouton bleu **"Update the stack"** en bas de la section et cochez la case **"Re-pull image and redeploy"** puis validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725285760778.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725285760778.png)

<p class="success-note">Vous venez de mettre à jour <b>Sonatype Nexus Repository</b> !</p>

# Désinstallation
- Rendez-vous dans l'onglet **"Containers"**, sélectionnez les conteneurs à supprimer (dans notre cas **sonatype_nexus-nexus-1**) puis cliquiez sur **"Remove"** en haut à droite, cochez **"Automatically remove non-persistent volumes"** et validez
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725372112206.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725372112206.png)
- Allez ensuite dans l'onglet **"Images"** et supprimez les images adéquates, dans notre cas **"sonatype/nexus3:latest"**
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725372153799.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725372153799.png)
  
<p class="info-note">Les networks vides seront automatiquement supprimés</p>
<p class="success-note">Vous venez de désinstaller <b>Diun</b> de votre système !</p>