---
title: Présentation de l’assistant AI dans Adobe Experience Platform
description: Découvrez l’assistant IA, ses nuances, ses cas d’utilisation et comment l’utiliser pour accélérer votre workflow avec Adobe Experience Platform et Real-time Customer Data Platform.
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: e90333d09585c8aa0ef176dcfc4717e86364fd54
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 15%

---

# Assistant AI dans Adobe Experience Platform

La vidéo suivante est destinée à vous aider à comprendre l’assistant AI.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

Lisez ce document pour en savoir plus sur l’assistant AI dans Adobe Experience Platform.

L’Assistant IA dans Adobe Experience Platform est une expérience conversationnelle que vous pouvez utiliser pour accélérer vos workflows dans les applications Adobe. Vous pouvez utiliser l’Assistant IA pour développer vos connaissances sur le produit, résoudre les problèmes ou rechercher des informations et trouver des informations opérationnelles. L’Assistant IA prend en charge Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

![Interface de l’assistant d’IA avec la première expérience utilisateur déclenchée.](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>Vous devez accepter un [contrat d’utilisateur](https://www.adobe.com/fr/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html) avant de pouvoir utiliser l’assistant AI. Le contrat utilisateur contient également le contrat bêta public. Cela vous permet d’utiliser des fonctionnalités supplémentaires de l’assistant d’IA lors de leur déploiement en version bêta.

+++Sélectionner pour afficher l’interface du contrat utilisateur

![Première page du contrat d’utilisation.](./images/user-agreement-1.png)

![Dernière page du contrat d’utilisation.](./images/user-agreement-2.png)

+++

## Présentation de l’assistant AI {#understanding-ai-assistant}

L’assistant AI répond à vos questions envoyées en interrogeant une base de données, puis en traduisant les données de la base de données en une réponse lisible par l’utilisateur.

Cette représentation interne des données sous-jacentes est également appelée **[!DNL Knowledge Graph]**. Il s’agit d’un réseau complet de concepts, de données et de métadonnées pour une réponse donnée.

Le [!DNL Knowledge Graph] se compose de sous-graphiques qui sont référencés chaque fois que les requêtes sont envoyées :

* Informations opérationnelles sur le client.
* Informations opérationnelles sur les clients dans divers méta-magasins.
* Documentation Experience League.

Il existe deux catégories de questions à prendre en compte avant d’interroger l’assistant AI :

### Connaissances du produit {#product-knowledge}

La connaissance des produits fait référence aux concepts et aux sujets reposant sur la documentation d’Experience League. Les questions relatives à la connaissance des produits peuvent être spécifiées de manière plus détaillée dans les sous-groupes suivants :

| Connaissances du produit | Exemples |
| --- | --- |
| Apprentissage par points | <ul><li>Quelle est la différence entre une identité et une clé primaire ou étrangère ?</li><li>Que sont les audiences semblables ?</li></ul> |
| Ouvrir la découverte | <ul><li>Comment exporter ce jeu de données ?</li><li>Existe-t-il des schémas pour les clients du secteur de la santé ?</li></ul> |
| Dépannage | <ul><li>Pourquoi ne puis-je pas activer un schéma détenu par Adobe pour le profil ?</li><li>Pourquoi ne puis-je pas supprimer un segment ?</li></ul> |

{style="table-layout:auto"}

Regardez la vidéo suivante pour plus d’informations sur les connaissances du produit Assistant AI :

>[!VIDEO](https://video.tv.adobe.com/v/3438032/?learn=on)

### Informations opérationnelles {#operational-insights}

Les informations opérationnelles se rapportent aux réponses que l’assistant AI génère sur vos objets de métadonnées (attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources), y compris les nombres, les recherches et l’impact de la parenté. Il n’examine aucune donnée du sandbox.

* De combien de jeux de données dispose-t-on ?
* Combien d’attributs de schéma n’ont jamais été utilisés ?
* Quelles audiences ont été activées ?

Vous pouvez poser des questions à l’assistant d’IA sur vos informations opérationnelles dans les domaines suivants :

| Domaine | Métadonnées prises en charge | Métadonnées non prises en charge |
| --- | --- | --- |
| Attributs | <ul><li>Recherche de nom d’attribut</li><li>Attribut - relation de schéma</li><li>Attribut - relation du jeu de données</li><li>Attribut - Relation d’audience</li><li>Attribut - relation de destination</li></ul> | <ul><li>Classe d’attribut</li><li>Journal</li><li>Statut d’obsolescence</li><li>Libellés</li><li>Valeur stockée dans les attributs</li></ul> |
| Audiences | <ul><li>Taille de l’audience</li><li>Type d’audience (diffusion en continu ou par lots)</li><li>Dates de création/modification</li><li>Statut d’activation</li><li>Nombre de profils</li><li>Dupliquer les audiences</li><li>Recherche de définition d’audience</li><li>Audience - Relation d’audience</li><li>Audience - Relation d’attributs</li><li>Audience - Relation du jeu de données</li><li>Audience - Relation de destination</li><li>Recherche de nom</li><li>Recherche par nom et ID | <ul><li>Chevauchements d’audience</li><li>Activation des audiences</li><li>Audience - relations de campagne</li><li>Journal</li><li>Créer/modifier</li><li>Libellés</li><li>Tendances de qualification des profils</li></ul> |
| Flux de données | <ul><li>Nombre de flux de données</li><li>Statut du flux de données</li><li>Flux de données - Relation du jeu de données</li><li>Flux de données - Relation source</li></ul> | <ul><li>Création/modification</li><li>Relations flux de données-lot</li><li>Ingérer le nombre de profils</li></ul> |
| Jeux de données | <ul><li>Nombre de jeux de données</li><li>Statut d’activation du profil</li><li>Date de création/modification</li><li>Jeu de données - Relation de schéma</li><li>Jeu de données - Relation d’audience</li><li>Relation jeu de données - attribut</li><li>Jeu de données - Relation de flux de données</li><li>Recherche de nom </li><li>Recherche par nom et ID</li></ul> | <ul><li>Journal</li><li>Créé par</li><li>Jeu de données - Relation par lots</li><li>Création/modification de jeu de données</li><li>Taille du jeu de données</li><li>Nombre de profils</li><li>Nombre de lignes</li><li>Recherche de valeur</li></ul> |
| Destinations | <ul><li>Nombre de destinations configurées</li><li>Relation destination-audience</li><li>Relation d’attributs de destination</li></ul> | <ul><li>Configuration du compte</li><li>Informations d’identification du compte</li><li>Profils uniques activés</li></ul> |
| Parcours | <ul><li>Comptages</li><li>Recherche de nom</li><li>Recherche par nom et ID</li><li>Statut du parcours</li><li>Statut de déclenchement (audience ou événements)</li><li>Dates de création/modification</li><li>Fréquence récurrente</li></ul> | <ul><li>Attributs - Relations de parcours</li><li>Journal</li><li>Création/modification</li><li>Créé par</li><li>Événements</li><li>Parcours - jeu de données</li><li>Parcours - schéma</li><li>Offres</li><li>Tendances de qualification des profils</li><li>Événements d’étape</li></ul> |
| Schémas | <ul><li>Nombre de schémas</li><li>Date de création/modification</li><li>Schéma - Relation des attributs</li><li>Schéma - Relation du jeu de données</li><li>Schéma - Relation d’audience</li><li>Statut d’activation du profil</li><li>Recherche de nom</li><li>Recherche par nom et ID</li></ul> | <ul><li>Journal</li><li>Création/modification</li><li>Créé par</li><li>Groupes de champs</li><li>Identités</li><li>Espaces de noms d’identité</li><li>Libellés</li><li>Nombre de profils</li></ul> |
| Sources | <ul><li>Comptes</li><li>Statut du compte</li><li>Flux de données actifs/inactifs pour chaque compte</li><li>Connecteur Source - Relation de flux de données</li><li>Compte Source - relation du flux de données</li></ul> | <ul><li>Informations d’identification du compte</li><li>Configuration du compte</li><li>Mesures d’ingestion de données</li><li>Nombre de profils</li><li>Source - relations par lots</li></ul> |

{style="table-layout:auto"}

Pour les questions relatives aux informations opérationnelles, les réponses peuvent ne pas refléter l’état actuel de l’interface utilisateur. Les données sur lesquelles reposent ces questions sont mises à jour toutes les 24 heures. Par exemple, les modifications apportées par les utilisateurs et utilisatrices dans Real-Time CDP pendant la journée sont synchronisées avec les entrepôts de données la nuit, puis répondent aux questions des utilisateurs et utilisatrices le matin. Vous devrez vous connecter à un sandbox pour vous renseigner sur des données spécifiques liées à des objets.

Regardez la vidéo suivante pour plus d’informations sur les informations opérationnelles de l’assistant IA :

>[!VIDEO](https://video.tv.adobe.com/v/3444034?learn=on&enablevpops&captions=fre_fr)

### Périmètre de la fonctionnalité {#feature-scope}

Actuellement, la portée de l’assistant AI est la suivante :

* [Connaissance des produits](./home.md#product-knowledge) : l’assistant AI peut répondre aux questions sur la connaissance des produits pour Experience Platform, Real-Time Customer Data Platform et Adobe Journey Optimizer. Vous pouvez également approfondir les rubriques de connaissance des produits Customer Journey Analytics, mais uniquement via l’interface utilisateur de Customer Journey Analytics.
* [Informations opérationnelles &#x200B;](./home.md#operational-insights) : vous pouvez poser des questions à l’assistant AI sur les informations opérationnelles relatives aux objets de données suivants : attributs, audiences, flux de données, jeux de données, destinations, parcours, schémas et sources.

## Étapes suivantes

Maintenant que vous avez une compréhension générale de l’assistant AI, vous pouvez procéder à et utiliser l’assistant AI pendant vos workflows. Pour plus d’informations, reportez-vous à la documentation suivante :

* [Guide de l’interface utilisateur de l’assistant AI](./ui-guide.md)
* [Accès aux fonctionnalités](./access.md)
* [Guide des questions](./questions.md)
* [Assistant Confidentialité, sécurité et gouvernance dans l’IA](./privacy.md)
* [FAQ](./faq.md)
