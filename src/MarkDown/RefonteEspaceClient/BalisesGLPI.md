@import "../../../style/styles_epitech_stage.less"

# Qu'est-ce que c'est ?

Les balises de notification dans GLPI (Gestionnaire Libre de Parc Informatique) sont des éléments dynamiques qui permettent de personnaliser le contenu des notifications envoyées par le système. Ces notifications peuvent être des emails ou des alertes internes envoyées à des utilisateurs, des techniciens, des demandeurs, etc., en fonction de certains événements ou actions au sein de GLPI, comme la création ou la clôture d’un ticket.

<p><img src="../../../assets/images/Doc/GLPI/Logo.png" alt="Description de l'image" style="margin: auto; width: 20%"></p>

## Ça sert à quoi ?

Les balises sont utilisées pour insérer automatiquement des informations spécifiques et contextuelles dans les messages envoyés par GLPI. Cela permet d'avoir des notifications claires, précises et adaptées à chaque situation sans avoir à écrire manuellement chaque message.

### Exemple de balises et leur utilisation

Voici quelques exemples de balises fréquemment utilisées dans GLPI, avec leur fonction :

- ##ticket.id## : Cette balise sera remplacée par l'identifiant unique du ticket.
- ##ticket.title## : Titre du ticket.
- ##ticket.description## : Description du ticket.
- ##user.name## : Nom de l'utilisateur concerné par l'action (demandeur, observateur, ou technicien).
- ##ticket.status## : État du ticket (en cours, résolu, fermé, etc.).
- ##ticket.sla## : Délai de résolution selon le SLA (Service Level Agreement).

### Exemple concret

Imaginons une notification de création de ticket avec les balises :

- Sujet : "Nouveau ticket : ##ticket.title## (##ticket.id##)"
- Message :
  - "Un nouveau ticket a été créé.
  - Numéro de ticket : ##ticket.id##
  - Titre : ##ticket.title##
  - Description : ##ticket.description##
  - Assigné à : ##user.name##
  - État actuel : ##ticket.status##."<br><br>

Lors de l'envoi de la notification, GLPI remplace ces balises par les informations réelles liées au ticket, par exemple :<br><br>

- Sujet : "Nouveau ticket : Problème d'imprimante (12345)"
- Message :
  - "Un nouveau ticket a été créé.
  - Numéro de ticket : 12345
  - Titre : Problème d'imprimante
  - Description : L'imprimante ne fonctionne plus.
  - Assigné à : Marie Dupont
  - État actuel : En cours."

## Pourquoi c'est cool ?

L'utilisation des balises de notification permet :

- Gain de temps : Évite de personnaliser manuellement chaque notification.
- Automatisation : Les notifications sont envoyées automatiquement aux personnes concernées, avec des informations pertinentes selon le contexte.
- Cohérence : Assure une homogénéité dans la communication via les notifications, ce qui améliore la gestion des incidents ou des demandes.

## Au final...

En résumé, les balises de notification dans GLPI servent à automatiser et personnaliser les messages envoyés par le système, afin d'améliorer la communication et le suivi des actions.
