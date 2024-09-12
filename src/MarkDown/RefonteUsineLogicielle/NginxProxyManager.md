@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Nginx Proxy Manager ?
Nginx Proxy Manager est une **interface graphique** pour gérer Nginx en tant que **serveur reverse proxy**. Il simplifie la configuration de Nginx en offrant une interface utilisateur intuitive, permettant de gérer facilement les **certificats SSL**, les **redirections**, et les **configurations d'hôtes virtuels**.

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725348098470.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725348098470.png)
## Nginx ?
Nginx, à la base, est un **serveur web** très performant qui peut également être utilisé pour **équilibrer la charge**, **servir du contenu statique** et **agir comme un reverse proxy**, ce qui signifie qu'il peut **transférer les demandes des utilisateurs vers d'autres serveurs**. Il est largement reconnu pour sa capacité à gérer un grand nombre de connexions simultanées avec une faible consommation de ressources, ce qui le rend idéal pour des applications à forte charge.
## Reverse Proxy ?
Un reverse proxy est un **serveur qui se place entre les clients (les utilisateurs finaux) et les serveurs backend (les serveurs où se trouvent les applications ou les sites web)**. Il **reçoit les requêtes des utilisateurs** et les **redirige vers les serveurs appropriés en interne**, tout en retournant les réponses aux utilisateurs. Ce qui fait que la sécurité de l'application web est assurée car aulieu d'aller sur http://10.2.1.70:3000 par exemple, nous pourrons aller sur https://code-repo.symexo.com, le reverse proxy va recevoir la demande et nous rediriger vers http://10.2.1.70:3000.

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725348999961-symexo-com.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725348999961-symexo-com.png)

# Installation
*Pour procéder à cette installation, nous allons nous servir de Portainer installé précédement...*
- Tout d'abord vous allez créer une nouvelle stack, lui donner un nom et coller le code ci-dessous dans l'éditeur de la stack :
```yaml
version: '3.8'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '443:443'
      - '81:81'

    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```
<p class="info-note">Dans ce compose, nous créons un service nommé <b>"app"</b> exposant les ports <b>80</b>, <b>443</b> et <b>81</b> avec les volumes <b>data</b> et <b>letsencrypt</b> et qui <b>se redémarre automatiquement tant qu'on ne l'arrête pas</b></p>

- Une fois le code collé vous pouvez cliquer sur le petit bouton bleu **"Deploy the stack"** et le conteneur sera lancé, vous pouvez maintenant aller dans l'onglet "Containers", vous verez votre conteneur. Pour s'y connecter il faudra cliquer sur le lien à droite contenant les ports, **443** correspond au port **HTTPS**, le **80** au **HTTP** et le **81** à **l'Interface admin de NPM**.
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725349675405.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725349675405.png)

<p class="success-note">Vous avez installé <b>Nginx Proxy Manager</b> !</p>

# Mise à jour
Pour ce faire, rien de plus simple ! Si vous avez mis la version "latest", vous pouvez faire comme suit, sinon, changez juste la version et faites la même chose !

- Rendez-vous dans votre stack Nginx Proxy Manager, dans **"Editor"**, puis cliquez sur le petit bouton bleu **"Update the stack"** en bas de la section et cochez la case **"Re-pull image and redeploy"** puis validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725285760778.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725285760778.png)

<p class="success-note">Vous venez de mettre à jour <b>Nginx Proxy Manager</b> !</p>


# Exemple de configuration
<p class="warning-note">Dans cette étape, nous allons configurer un proxy host, attention, pour cela vous devez avez votre DNS de configuré avec votre application !</p>

## créer un certificat SSL
<p class="warning-note">Attention à en avoir un de fournit au préalable !</p>

- Pour passer en HTTPS vous allez devoir créer un **certificat SSL sur Nginx Proxy Manager**, pour ce faire vous allez vous rendre sur l'onglet **"SSL Certificates"**
- Maintenant que vous y êtes, vous allez cliquer sur le buton **Add SSL Certificate"** et sélectionner **"Custom"**
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725350614401.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725350614401.png)
- Une fois ici, vous allez lui donner un **nom**, importer une **clé de certificat** et un **certificat**. Enfin, cliquez sur le bouton **save**.
<p class="info-note">La clé est un fichier <b>.key</b> et le certificat un <b>.crt</b></p>
<p class="success-note">Super, vous avez maintenant un <b>certificat SSL</b> !</p>

## Création d'un Proxy Host
- Rendez-vous sur le **Dashboard** puis dans **Proxy Host**.
- Un fois dans le bon menu, vous allez cliquer sur le bouton **"Add Proxy Host"**.
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725351016016.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725351016016.png)
- Une fois sur l'onglet de configuration, vous allez compléter **Domain Names** avec le l'**URL que vous avez paramétré sur votre DNS**, **Forward Hostname/IP** avec l'**IP de votre application** et le **Forward Port** avec le **port de votre application**.
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725351196803.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725351196803.png)
- Maintenant vous allez vous rendre dans l'onglet **"SSL"** du menu de configuration du Proxy Host et Sélectionner celui que vous avez créer précédemment. Puis vous enregistrez.
- À présent, vous pouvez tester votre **Proxy Host** en essayant d'**accéder au nom de domaine** paramétré.

<p class="success-note">Vous avez configurer un <b>Proxy Host</b> avec un <b>Certificat SSL</b> sur <b>Nginx Proxy Manager</b></p>

# Désinstallation
- Rendez-vous dans l'onglet **"Containers"**, sélectionnez les conteneurs à supprimer (dans notre cas **nginx_proxy_manager-app-1**) puis cliquiez sur **"Remove"** en haut à droite, cochez **"Automatically remove non-persistent volumes"** et validez.
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725351616444.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725351616444.png)
- Allez ensuite dans l'onglet **"Images"** et supprimez les images adéquates, dans notre cas **"jc21/nginx-proxy-manager:latest**"
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725351669527.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725351669527.png)
  
<p class="info-note">Les networks vides seront automatiquement supprimés</p>
<p class="success-note">Vous venez de désinstaller <b>Nginx Proxy Manager</b> de votre système !</p>