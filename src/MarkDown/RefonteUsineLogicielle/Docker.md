@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Ça sert à quoi ?
Docker est une plateforme logicielle qui permet de créer, déployer et gérer des applications dans des conteneurs. Ce qui évite de créer des machines virtuelles à ne plus savoir quoi en faire !

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725269744260.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725269744260.png)

## C'est quoi un conteneur ?
Les conteneurs sont des environnements isolés qui contiennent tout ce dont une application a besoin pour fonctionner, y compris le code, les bibliothèques, et les dépendances qui sont déployés à partir d'images docker. Au final les conteneurs sont des sortes de boites dans lesquelles on va venir ranger nos applications. Ce qui permet une portabilité sans pareille, nous pouvons déplacer notre application d'une machine à une autre tant que celle-ci à docker d'installé.

## C'est quoi une image Docker ?
Une image Docker est un modèle immuable qui contient tout ce qui est nécessaire pour exécuter une application. Cela inclut le code source de l'application, les bibliothèques, les dépendances, les fichiers de configuration, et le système d'exploitation minimal requis pour que l'application fonctionne.

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725270097181.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725270097181.png)
<p class="info-note">Les exmples suivants seront exécutés sur un environnement Linux Debian 12 en utilisant le dépot <b>apt</b></p></div>

# Installation
<p class="info-note">Si vous n'êtes pas root sur votre système, vous devrez précéder la plupart des commandes par "<b>sudo</b>" pour vous octroyer les droits.</p>

1) Installer **dépot apt Docker**
```bash
# Ajout de la clé GPG officielle de Docker:
 apt-get update
 apt-get install ca-certificates curl
 install -m 0755 -d /etc/apt/keyrings
 curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
 chmod a+r /etc/apt/keyrings/docker.asc

# Ajout du dépot depuis les sources apt
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
   tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
```

2) Intallation de la dernière version des paquets Docker
```bash
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

3) Vérification d'installation en exécutant l'image **hello-world**
```bash
docker run hello-world
```
Cette commande va installer une image de test et l'exécuter dans un conteneur. Quand le conteneur s'exécute, il affiche un message de confirmation et s'arrête.

Vous devriez avoir quelque chose comme ça :
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725270184914.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725270184914.png)
<p class="success-note">Vous avez installé Docker !</p>

# Mise à Jour
Pour ce faire, rien de plus simple
```bash
apt-get update
apt-get upgrade -y
apt-get dist-upgrade -y
apt-get autoremove -y
```
ou pour aller plus vite
```bash
apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get autoremove -y
```

# Désinstallation
1) Désintallation du moteur Docker, CLI, Conteinerd, et les paquets Docker Compose
```bash
apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

2) Les images, conteneurs, volumes, ou configurations customisées dans votre hôte ne sont pas automatiquement retirées. Pour supprimer toutes les images, conteneurs, et volumes
```bash
rm -rf /var/lib/docker
rm -rf /var/lib/containerd
```
<p class="success-note">Vous avez supprimé Docker et toutes ses configuration !</p>