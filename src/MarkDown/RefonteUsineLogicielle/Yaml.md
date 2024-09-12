@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

## Ça sert à quoi ?

Le YAML est souvent utilisé pour la configuration de logiciels, le stockage de données et la transmission d'informations entre systèmes.

- Fichiers de configuration : Beaucoup d'outils et de logiciels modernes (comme Docker, Kubernetes, Ansible, et bien d'autres) utilisent des fichiers YAML pour définir leurs configurations.
  - Exemple : La configuration d’un déploiement Docker est souvent décrite en YAML.
- Sérialisation de données : YAML est utilisé pour transmettre des données entre systèmes ou stocker des informations dans des fichiers.
- Gestion d'infrastructure : Dans l'administration système et le DevOps, YAML est couramment utilisé pour définir l'infrastructure sous forme de code, facilitant l'automatisation et la gestion à grande échelle.

## Pourquoi c'est cool ?

- Format Lisible pour les Humains :
  - Le YAML est conçu pour être facilement compréhensible par les humains. Comparé à d'autres formats comme JSON ou XML, il est moins verbeux et plus lisible.
  - Il utilise l'indentation (comme en Python) pour structurer les données, ce qui le rend intuitif.
- Structure et Syntaxe :
  - Clés-Valeurs : Les données sont généralement exprimées sous forme de paires clé-valeur.

  ```yaml
  nom: Pierre
  age: 30
  ville: Paris
  ```

  - Listes : On peut représenter des listes simplement avec des tirets (-).

  ```yaml
  fruits:
    - pomme
    - banane
    - orange
  ```

  - Hiérarchies : Les données peuvent être imbriquées grâce à l'indentation.

  ```yaml
  adresse:
    rue: 123 Rue Principale
    ville: Paris
    code_postal: 75000
  ```
