---
title: Présentation de l’assistant AI dans Adobe Experience Platform
description: Découvrez l’assistant IA, ses nuances, ses cas d’utilisation et comment l’utiliser pour accélérer votre workflow avec Adobe Experience Platform et Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: e8939132c1508e1dfc4028e6c8ff23662d6c2b2b
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 7%

---

# Assistant IA dans Adobe Experience Platform

Lisez ce document pour en savoir plus sur l’assistant d’IA dans Adobe Experience Platform.

L’assistant d’IA dans Adobe Experience Platform est une expérience conversationnelle que vous pouvez utiliser pour accélérer vos workflows dans les applications Adobe. Vous pouvez utiliser l’assistant d’IA pour mieux comprendre les connaissances sur les produits, résoudre les problèmes ou rechercher des informations et trouver des informations opérationnelles. L’assistant d’IA prend en charge Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

![Interface de l’assistant d’IA avec la première expérience utilisateur déclenchée.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Vous devez accepter un [accord utilisateur](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) avant de pouvoir utiliser l’assistant d’IA. Le contrat d’utilisation contient également le contrat bêta public. Vous pouvez ainsi utiliser d’autres fonctions d’assistant d’IA au fur et à mesure qu’elles se déploient en version bêta.

+++Sélectionner pour afficher l’interface des accords utilisateur

![La première page du contrat utilisateur.](./images/user-agreement-1.png)

![Dernière page du contrat utilisateur.](./images/user-agreement-2.png)

+++

## Présentation de l’assistant d’IA {#understanding-ai-assistant}

L’assistant d’IA répond aux questions que vous avez envoyées en interrogeant une base de données, puis en traduisant les données de la base de données en une réponse lisible.

Cette représentation interne des données sous-jacentes est également appelée **[!DNL Knowledge Graph]** - un réseau complet de concepts, de données et de métadonnées pour une réponse donnée.

La variable [!DNL Knowledge Graph] se compose de sous-graphiques qui sont référencés chaque fois que des requêtes sont envoyées :

* Informations sur les opérations du client.
* Informations sur les opérations des clients dans divers méta-magasins.
* Documentation Experience League.

Il existe deux types de questions à prendre en compte avant d’interroger l’assistant d’IA :

### Connaissances produit {#product-knowledge}

Les connaissances sur les produits se rapportent aux concepts et aux sujets basés sur la documentation Experience League. Les questions relatives aux connaissances sur les produits peuvent être spécifiées plus en détail dans les sous-groupes suivants :

| Connaissances produit | Exemples |
| --- | --- |
| Apprentissage pointé | <ul><li>Quelle est la différence entre une identité et une clé primaire ou étrangère ?</li><li>Comment est calculé la richesse des profils ?</li></ul> |
| Découverte ouverte | <ul><li>Comment exporter ce jeu de données ?</li><li>Y a-t-il des schémas pour les clients du secteur de la santé ?</li></ul> |
| Dépannage | <ul><li>Pourquoi ne puis-je pas activer un schéma détenu par Adobe pour Profile ?</li><li>Pourquoi ne puis-je pas supprimer un segment ?</li></ul> |

{style="table-layout:auto"}

### Informations opérationnelles {#operational-insights}

>[!IMPORTANT]
>
>Les réponses sur les informations opérationnelles sont en version bêta. Toute personne ayant accès à la variable **Affichage des informations opérationnelles** La permission aura accès aux réponses sur les informations opérationnelles.

Les informations opérationnelles se rapportent aux réponses générées par l’assistant d’IA au sujet de vos objets de métadonnées (attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources), y compris les décomptes, les recherches et l’impact sur la traçabilité. Il ne tient compte d’aucune donnée dans l’environnement de test.

* Combien de jeux de données ai-je ?
* Combien d’attributs de schéma n’ont jamais été utilisés ?
* Quelles audiences ont été activées ?

Vous pouvez poser des questions à l’assistant d’IA sur vos informations opérationnelles dans les domaines suivants :

| Domaine | Métadonnées prises en charge |
| --- | --- |
| Attributs | <ul><li>Recherches de nom d’attribut</li><li>Attribut - relation de schéma</li><li>Attribut - relation entre les jeux de données</li><li>Attribut - relation d’audience</li><li>Attribut - relation de destination</li><li>Attributs non utilisés</li></ul> |
| Audiences | <ul><li>Taille de l’audience</li><li>Type d’audience (diffusion en continu ou par lot)</li><li>Dates de création/modification</li><li>État de l’activation</li><li>Nombre de profils</li><li>Duplication d&#39;audiences</li><li>Recherches de définitions d’audience</li><li>Audience - relation d’attribut</li><li>Audience - relation entre les jeux de données</li><li>Audience - relation de destination</li><li>Règles InSegment</li><li>Nommer les recherches</li><li>Recherches de nom et d’identifiant |
| Flux de données | <ul><li>Nombre de flux de données</li><li>Statut du flux de données</li><li>Flux de données : relation entre les jeux de données</li><li>Flux de données - relation source</li></ul> |
| Jeux de données | <ul><li>Nombre de jeux de données</li><li>État d’activation du profil</li><li>Date de création/modification</li><li>Jeu de données - relation de schéma</li><li>Jeu de données - relation avec l’audience</li><li>Jeu de données - relation d’attribut</li><li>Jeu de données - relation de flux de données</li><li>Nommer les recherches </li><li>Recherches de nom et d’identifiant</li></ul> |
| Destinations | <ul><li>Nombre de destinations configurées</li><li>Destination - relation avec l’audience</li><li>Relation d’attribut de destination</li></ul> |
| Parcours | <ul><li>Comptages</li><li>Nommer les recherches</li><li>Recherches de nom et d’identifiant</li><li>Statut du parcours</li><li>État déclenché (audience par rapport aux événements)</li><li>Dates de création/modification</li><li>Fréquence récurrente</li></ul> |
| Schémas | <ul><li>Nombre de schémas</li><li>Date de création/modification</li><li>Type de classe de schéma</li><li>Schéma - relation d’attribut</li><li>Schéma - relation avec le jeu de données</li><li>Schéma - relation avec l’audience</li><li>État d’activation du profil</li><li>Nommer les recherches</li><li>Recherches de nom et d’identifiant</li></ul> |
| Sources | <ul><li>Nombre de comptes</li><li>État du compte</li><li>Flux de données actifs/inactifs pour chaque compte</li><li>Connecteur source - relation de flux de données</li><li>Compte source - relation de flux de données</li></ul> |

{style="table-layout:auto"}

Pour les questions d’informations opérationnelles, les réponses peuvent ne pas refléter l’état actuel de l’interface utilisateur. Les données qui appuient ces questions sont mises à jour toutes les 24 heures. Par exemple, les modifications apportées par les utilisateurs dans Real-Time CDP pendant la journée sont synchronisées avec les entrepôts de données la nuit, puis elles deviennent disponibles pour les questions des utilisateurs le matin. Vous devrez vous connecter à un environnement de test pour obtenir des informations sur des données spécifiques liées aux objets.

### Périmètre de la fonctionnalité {#feature-scope}

Actuellement, la portée de l’assistant d’IA est la suivante :

* [Connaissances produit](./home.md#product-knowledge): l’assistant d’IA peut répondre aux questions sur les connaissances des produits pour Experience Platform, Real-time Customer Data Platform et Adobe Journey Optimizer. Vous pouvez également approfondir les connaissances sur les produits pour Customer Journey Analytics, mais uniquement via l’interface utilisateur de Customer Journey Analytics.
* [Connaissances opérationnelles](./home.md#operational-insights): vous pouvez poser des questions à l’assistant d’IA sur les informations opérationnelles des objets de données suivants : attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources.

## Étapes suivantes

Maintenant que vous connaissez tous l’assistant d’IA, vous pouvez continuer et utiliser cet assistant pendant vos workflows. Pour plus d’informations, reportez-vous à la documentation suivante :

* [Guide de l’interface utilisateur de l’assistant IA](./ui-guide.md)
* [Accès aux fonctionnalités](./access.md)
* [Guide des questions](./questions.md)
* [Confidentialité, sécurité et gouvernance dans l’assistant d’IA](./privacy.md)
* [FAQ](./faq.md)
