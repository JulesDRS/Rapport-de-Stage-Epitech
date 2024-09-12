@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Sonatype ?
Sonatype est une entreprise spécialisée dans **la gestion et la sécurité des composants logiciels**, principalement des bibliothèques open-source, utilisés dans le développement d'applications. Leur suite d'outils est conçue pour **aider les organisations à gérer efficacement leurs dépendances logicielles**, à s'assurer que les composants utilisés sont sécurisés, et à maintenir la conformité avec les normes de développement.

## Nexus Repository Manager ?
Nexus Repository Manager est un **gestionnaire de dépôt** qui permet aux équipes de développement de **stocker**, de **partager** et de **gérer les artefacts logiciels**, **comme les bibliothèques** et **les dépendances**. Il prend en charge divers formats, tels que Maven, npm, Docker, et bien d'autres.

# Installation
*Pour procéder à cette installation, nous allons nous servir de Portainer installé précédement...*
- Tout d'abord vous allez créer une nouvelle stack, lui donner un nom et coller le code ci-dessous dans l'éditeur de la stack :
```yaml
version: "3"
services:
  nexus:
    image: sonatype/nexus3
    restart: always
    volumes:
      - "nexus-data:/sonatype-work"
    ports:
      - "8081:8081"
      - "8085:8085"
volumes:
  nexus-data: {}
```
<p class="info-note">Dans ce compose, nous instancions une image et un conteneur <b>Sonatype Nexus 3</b> pour stocker les utilisateurs et les artéfacts que nous créront plus tard dans <b>Nexus Repository</b></p>

- Une fois le code collé vous pouvez cliquer sur le petit bouton bleu **"Deploy the stack"** et le conteneur sera lancé, vous pouvez maintenant aller dans l'onglet "Containers", vous verez votre contreneur **Sonatype Nexus**:
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725367400806.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725367400806.png)
- Vous allez maintenant vous rendre sur votre Sonatype Nexus en cliquant sur le lien **"8081:8081"** à droite<br>
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725367602076.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725367602076.png)
- Cependant, pour vous connecter il va vous falloir trouver le mdp dans le chemin indiqué quand vous essayez de vous connecter, pour celà il va falloir entrer dans le volume du conteneur pour le trouver, pour ma part il est au chemin suivant : ***/nexus-data/admin.password*** <br>
Pour ouvrir un bash dans le conteneur et y pénétrer vous pouvez utiliser la commande suivante :
```bash
docker exec -it <container_name_or_id> bash
```

<p class="success-note">Vous avez installé et configuré <b>Sonatype Nexus Repository Manager</b> !</p>

# Configuration (facultatif)
Voyons maintenant un petit exemple de configuration que j'ai fais pour l'usine logicielle et que vous pouvez tout à fais suivre.<br>

Une fois que vous êtes connectés, vous devriez pourvoir accéder à l'onglet de configuration [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725538313089.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725538313089.png)

Une fois à l'intérieur, nous pouvon commencer...

- Premièrement, vous allez vous rendre dans l'onglet **"Repositories"** dans la liste déroulande du même nom.<br> Une fois dedans, vous pouvez voir qu'il y a déjà des dépots créés par défaut, nous n'allons pas nous en occuper car nous allons créer les notres en cliquant sur **"+ Create repository"**
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725538518533.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725538518533.png)

- Vous allez commencer par créer un **"maven2 (proxy)"**, tout ce que vous avez à faire est lui donner un nom et un URLdu dépot distant souhaité. Le proxy va être très utile, car quand nous allons demander les dépendances à celui-ci, s'il ne les trouve pas dans le groupe dans lequel il est (que nous créeront plus tard), il va directement aller les chercher sur le dépot dont vous avez mis l'URL, personellement j'ai mis ***"https://repo1.maven.org/maven2/"***
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725538892774.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725538892774.png)

Une fois ces champs remplis, vous pouvez valider la création.

- Ensuite vous allez créer un dépot **"maven2 (hosted)"**, une fois dans son menu de création il y aura plusieurs paramètres à régler : Premièrement son nom, ensuite préciser si ce dépot va être destiné à des releases ou des snaoshots, dans notre cas nous allons l'appeller **"symexo-maven-release"** dire qu'il va recevoir des **releases**.
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725539154249.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725539154249.png)

- Une fois celui-ci créé, nous allons en faire un autre qui pour ma part sera destiné à recevoir des **snapshots** et dont le nom sera **"symexo-maven-snapshots"**. mais outre ces deux paramètre, cette fois nous allons devoir en modifier un autre, celui qui dit qu'on pourra poster deux fois la même version. Pour release nous ne l'avons pas toucher car nous voulons qu'il y ait seulement les versions propres et qu'elles ne soient pas en doublons !
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725539351493.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725539351493.png)

- Et finalement, nous allons créer le groupe, pour celà, vous allez créer une instance **"maven2 (group)"**, lui donner un nom, lui dire que dans le groupe il y aura et des releases et des snapshots en sélectionnant l'option **"mixed"** et enfin, mettre tous les dépots que vous souhaitez, dont le porxy, dans le groupe !
[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725540265670.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725540265670.png)

<p class="success-note">Vous avez configurer un environnement <b>Sonatype</b> !</p>

# Mise à jour
Pour ce faire, rien de plus simple ! Si vous avez mis la version "latest", vous pouvez faire comme suit, sinon, changez juste la version et faites la même chose !

- Rendez-vous dans votre stack Sonatype Nexus, dans **"Editor"**, puis cliquez sur le petit bouton bleu **"Update the stack"** en bas de la section et cochez la case **"Re-pull image and redeploy"** puis validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725285760778.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725285760778.png)

<p class="success-note">Vous venez de mettre à jour <b>Sonatype Nexus Repository</b> !</p>

# Désinstallation
- Rendez-vous dans l'onglet **"Containers"**, sélectionnez les conteneurs à supprimer (dans notre cas **sonatype_nexus-nexus-1**) puis cliquiez sur **"Remove"** en haut à droite, cochez **"Automatically remove non-persistent volumes"** et validez
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725369965092.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725369965092.png)
- Allez ensuite dans l'onglet **"Images"** et supprimez les images adéquates, dans notre cas **"sonatype/nexus3:latest"**
  [![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725369921782.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725369921782.png)
  
<p class="info-note">Les networks vides seront automatiquement supprimés</p>
<p class="success-note">Vous venez de désinstaller <b>Sonatype Nexus Repository</b> de votre système !</p>