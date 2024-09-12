@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Ça sert à quoi ?
Comme son nom l'indique, c'est un **transporteur de conteneurs**, qui permet de gérer tout votre environnement Docker depuis une interface web, que ce soit les conteneurs, mais aussi les images, les stacks, les networks, volumes... C'est un outil tout en un de Développement Opérationnel aka DevOps Docker.

## C'est quoi des stacks ?
Les stacks, aussi appelées **"Docker Compose"** sont des fichiers de **configuration de services docker**, autrement dit ce sont des géniteurs d'images et de conteneurs Docker. Dans ces fichiers nous utiliserons des **images** pour configurer des **conteneurs** et les lier à des **volumes** ou des **networks** pour créer un système ou même un écosystème complet et fonctionnel pouvant être, grâce à ce fichier **déployé et redéployé à guise** sans difficultées !<br>

Ci-dessous, nous avons une stack qui contient 3 services, un Redis, un Apache et un Postgres et chaque service, via son image, va créer ses conteneurs

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725279178148.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725279178148.png)

## C'est quoi des networks ?
Les Networks sont des **centres de connexion entre différents conteneurs**, les permettant de communiquer dans un réseau fermé et sécurisé plus facilement et à leur guise.

Dans l'exemple ci-dessous, nous pourrons appeller l'App A non pas par son IP par exemple, mais pas le nom de son conteneur : **http://10.2.12.70:80 --> http://AppB:80**
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725278737266.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725278737266.png)

## C'est quoi des volumes ?
Les volumes sont des **espaces de stockages** alloués à des conteneurs pouvant être **partagés ou non selon les situations**. C'est un espace ou ceux-ci vont venir stocker toutes les informations dont ils disposent, celles qu'ils créeront et celles dont ils ont besoin.

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725278663745.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725278663745.png)

<p class="info-note">Les exmples suivants seront exécutés sur un environnement Linux <b>Debian 12</b></p>

# Installation
<p class="info-note">Si vous n'êtes pas root sur votre système, vous devrez précéder la plupart des commandes par <b>"sudo"</b> pour vous octroyer les droits.</p>

Très simple cette fois-ci, nous avons juste à exécuter la commande suivante :
```bash
docker run -d -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```

Cette commande va lancer un conteneur se nommant **"portainer"** exposant le port **9000** en se basant sur l'image **"portainer/portainer-ce:latest"** et stoquant ses informations dans le volume **"/data"** du conteneur et **"/portainer_data"** sur votre machine !
<p class="info-note"><b>"portainer/portainer-ce:latest"</b> va aller chercher sur le dépôt <b>"portainer-ce"</b> appartenant à <b>"portainer"</b> l'image <b>latest</b> qui correspond à la <b>dernière version</b> définie "latest" de celle-ci</p>
<p class="success-note">Vous venez d'installer et de paramétrer la dernière version de Portainer !</p>
<p class="warning-note">Dans les prochains chapitres, nous n'allons plus utiliser l'invite de commande pour gérer notre environnement Docker mais le Portainer que nous venons d'installer !</p>

# Mise à jour
Pour celà, nous allons devoir **arrêter le conteneur, le supprimer, réimporter l'image et le relancer...** Mais pas d'inquiétudes, les informations ne seront pas perdues vu que vous n'avez pas supprimer son volume, il vous suffit de mettre le même que vous aviez paramétrés avant et tout ira bien !
```bash
docker stop portainer
docker rm portainer
docker pull portainer/portainer-ce:latest

docker run -d -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
```
<p class="success-note">Et voilà ! Vous avez mis à jour Portainer et toutes ses données ont été conservées !</p>

# Désinstallation
Cette désinstallation sera un peu plus compliquée que celle de Docker, il va falloir **arrêter et supprimer le conteneur, supprimer son image, supprimer ses volumes** puis enfin nous l'aurons désinstaller totalement...<br>
Vous pouvez faire comme suit :

1) Arrêt et suppression du conteneur
- **Arrêtez le et supprimez le** :
```bash
docker stop portainer
docker rm portainer
```
ou pour faire plus rapide
```bash
docker stop portainer && docker rm portainer
```

2) Suppression de l'image de Portainer
- **Listez les images** présentes sur votre système et **récupérez l'ID** de celle qui contient Portainer en utilisant la commande suivante :
```bash
docker images
```
- Supprimez-la en utilisant l'ID récupéré :
```bash
docker rmi ${ID_or_NAME}
```

3) Suppression des volumes

Si vous avez fais la même configuration de volume que ci-dessus, vous n'avez qu'a exécuter la commande ci-dessous, sinon remplacez le volume que j'ai mis par le votre
```bash
rm -rf portainer_data:/data
```

<p class="success-note">Vous avez désintaller Portainer et toutes ses données !</p>

<p class="info-note">Je ne supprime pas /var/run/docker.sock car <b>ce n'est pas un volume</b> même s'il est considéré comme tel, c'est un fichier qui en bref, <b>répertorie tous les conteneurs docker</b>, ce qui permet entre autre que portainer contrôle même les conteneurs qui ne sont pas crées via lui-même</p>