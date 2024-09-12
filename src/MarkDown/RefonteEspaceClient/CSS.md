@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

Le CSS, ou "Cascading Style Sheets" (feuilles de style en cascade en français), est un langage utilisé pour décrire la présentation d'un document écrit en HTML ou en XML.

<p><img src="../../../assets/images/Doc/CSS/Logo.png" alt="Description de l'image" style="margin: auto; width: 20%"></p>

## Ça sert à quoi ?

#### Mise en forme du texte :

CSS permet de définir les polices, les tailles de texte, les couleurs, l'espacement des lignes, les marges, etc.

#### Disposition des éléments :

Il permet de placer et d'aligner les éléments sur la page, de définir des mises en page flexibles ou en grille, et de gérer la position des éléments de manière précise.

#### Couleurs et arrière-plans :

CSS permet de définir les couleurs de fond, les images de fond, et les couleurs des éléments de la page.

#### Effets et animations :

CSS peut être utilisé pour créer des effets de survol, des transitions douces entre les états des éléments, et des animations pour améliorer l'interactivité de la page.

#### Responsivité :

Avec le CSS, on peut adapter le design d'une page web pour qu'il soit agréable à utiliser sur différents appareils (ordinateurs, tablettes, téléphones mobiles).<br><br>

### Exemples

Voici quelques exemples de code CSS qui montrent comment styliser divers éléments d'une page web :

#### Changer la couleur et la taille du texte

Pour définir la couleur du texte d'un paragraphe en bleu et la taille de la police à 18 pixels :

```css
p {
  color: blue;
  font-size: 18px;
}
```

#### Ajouter un arrière-plan et changer la couleur du texte

Pour définir une couleur de fond et changer la couleur du texte d'un titre (h1) en blanc :

```css
h1 {
  background-color: black; /* couleur de fond */
  color: white; /* couleur du texte */
  padding: 10px; /* espacement interne */
}
```

#### Mettre en place une mise en page avec Flexbox

Pour aligner des éléments en ligne et les centrer horizontalement à l'aide de Flexbox :

```css
.container {
  display: flex; /* Activer Flexbox */
  justify-content: center; /* Centrer horizontalement */
  align-items: center; /* Centrer verticalement */
  height: 200px; /* Hauteur du conteneur */
  border: 1px solid #ccc; /* Bordure grise */
}
```
