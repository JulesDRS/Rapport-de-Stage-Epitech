@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

Le HTML (HyperText Markup Language) est un langage de balisage utilisé pour structurer et présenter le contenu des pages web.

<p><img src="../../../assets/images/Doc/HTML/Logo.png" alt="Description de l'image" style="margin: auto; width: 20%"></p>

## Ça sert à quoi ?

Il permet de définir des éléments comme les titres, les paragraphes, les liens, les images, les tableaux, et d'autres composants qui composent une page web.

Voici quelques éléments clés du HTML et son utilité :

### Structure d'une page web
Le HTML organise la structure de base d'une page web. Par exemple, il indique où se trouvent le titre, les sous-titres, les paragraphes de texte, et autres. Il est composé de balises qui délimitent chaque élément. Chaque balise HTML est entourée d'angle-brackets (< >).

Exemple d'une structure de base :

```html
<html>
  <head>
    <title>Ma première page</title>
  </head>
  <body>
    <h1>Bienvenue sur ma page</h1>
    <p>Ceci est un paragraphe.</p>
  </body>
</html>
```

### Affichage des contenus multimédias

Le HTML permet également d'inclure des images, des vidéos, des fichiers audio, et des animations dans une page web. Exemple d'insertion d'une image :

```html
<img src="mon_image.jpg" alt="Description de l'image">
```

### Création de liens hypertextes

L'un des points forts du HTML est sa capacité à créer des liens vers d'autres pages ou sites web. C'est ce qui permet la navigation entre différentes pages. Exemple de lien :

```html
<a href="https://www.exemple.com">Visitez cet exemple</a>
```

### Tables et listes

HTML permet également d'organiser les informations sous forme de tables ou de listes, facilitant ainsi la présentation de données structurées.

#### Exemple de liste non ordonnée :

```html
<ul>
  <li>Élément 1</li>
  <li>Élément 2</li>
</ul>
```

#### Exemple de table :

```html
<table>
  <tr>
    <th>Nom</th>
    <th>Âge</th>
  </tr>
  <tr>
    <td>Marie</td>
    <td>30</td>
  </tr>
</table>
```

### Compatibilité avec d'autres langages

Bien que le HTML définisse la structure de la page, il est souvent utilisé avec d'autres technologies web :

- CSS (Cascading Style Sheets) pour la mise en page et le design.
- JavaScript pour rendre la page interactive (par exemple, des boutons cliquables, des animations dynamiques).

## Au final...

Le HTML est la pierre angulaire du web. Il permet de construire des pages en définissant la structure et le contenu, tandis que des technologies comme le CSS et le JavaScript améliorent l'apparence et les fonctionnalités interactives.
