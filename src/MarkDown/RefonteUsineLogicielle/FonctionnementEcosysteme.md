@import "../../../style/styles_epitech_stage.less"

# Écosystème Usine Logicielle V2

[![](https://connaissances.symexo.com/uploads/images/gallery/2024-09/scaled-1680-/image-1725376105701.png)](https://connaissances.symexo.com/uploads/images/gallery/2024-09/image-1725376105701.png)

1) Le code est **Push sur Gitea**
2) Celui-ci passe par les **Gitea Actions**, un Workflow s'exécute et :
   - Vérifie la **compilation du Code**
   - **Exécute les test** si ceux-cis sont paramétrés
3) Si le build et les tests sont passés, le Workflow passe à l'étape suivante et :
   - **Envoie les artéfacts sur Sonatype Nexus Repository Manager**
   - **Envoie le code sur SonarQube** pour une analyse de qualité de code