---
title: Démarrage rapide avec Launch
seo-title: 'SDK Web d’Adobe Experience Platform : démarrage rapide avec Launch'
description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
seo-description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 27%

---


# Bienvenue

Ce guide vous guide tout au long des différentes manières de configurer le SDK Web de Adobe Experience Platform dans Launch. Pour utiliser cette fonctionnalité, vous devez être placé sur la liste autorisée. Si vous souhaitez monter sur la liste d&#39;attente, veuillez contacter votre CSM.

- Vous devez disposer d’un [domaine propriétaire (CNAME)](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html) activé. Si vous disposez déjà d’un CNAME pour Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionnent sans CNAME, mais vous en avez besoin avant de commencer la production.
- Avoir droit à Adobe Experience Platform. Si vous n’avez pas acheté Platform, l’Adobe vous fournira la Fondation Experience Platform Data Services pour une utilisation limitée avec le SDK sans frais supplémentaires.
- Vous devez utiliser la dernière version du service d’identifiant visiteur.

## Préparation d’un Schéma

L&#39;Experience Platform Edge Network prend les données au format XDM. XDM est un format de données qui vous permet de définir des schémas. Le schéma définit comment le réseau Edge prévoit que les données seront formatées. Pour envoyer des données, vous devez définir votre schéma.

1. [Création d’un schéma](../../xdm/tutorials/create-schema-ui.md)
2. ajoutez le [!DNL Web SDK ExperienceEvent] mixin AEP au schéma que vous avez créé.
3. Créez un jeu de données à partir du schéma que vous avez créé.

La vidéo suivante est destinée à vous aider à créer un schéma, un jeu de données et un connecteur source de flux continu pour vos [!DNL Web SDK] données.


>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

Connectez-vous à Launch et installez l’extension `AEP Web SDK`. Lorsque vous installez le SDK, vous êtes invité à configurer l’extension. Entrez l’ID de configuration que vous avez demandé ci-dessus. L’extension renseigne automatiquement l’ID d’organisation.


Pour plus d’informations sur les différentes options de configuration, voir [Configuration du SDK](../fundamentals/configuring-the-sdk.md).

## Création d’un ID de configuration

Vous pouvez créer un ID de configuration à l’aide de l’outil [de configuration](../fundamentals/edge-configuration.md) edge dans Launch. Cela vous permet de permettre au réseau Edge d&#39;envoyer des données aux différentes solutions. Vous trouverez des informations détaillées sur la manière de trouver chaque option dans la page Outil [de configuration](../fundamentals/edge-configuration.md) Edge.

>[!NOTE]
>
>Votre organisation doit être placée sur la liste autorisée pour cette fonctionnalité. Veuillez contacter votre CSM pour qu&#39;il soit mis sur la liste pour une liste autorisée éventuelle.

## Créer un élément de données basé sur votre Schéma

Dans Lancer, créez un élément de données qui référence le schéma en modifiant l’extension en SDK Web AEP et en définissant le type sur `XDM Object`. Cela charge votre schéma et vous permet de mapper des éléments de données dans différentes parties du schéma.

![Elément Date de lancement](../../assets/edge_data_element.png)

## Envoi d’un événement

After the extension is installed, start sending events by adding a `sendEvent` action from the AEP Web SDK extension to a rule. ajoutez l’élément de données que vous venez de créer au événement en tant que données XDM. adobe vous recommande d’envoyer au moins un événement chaque fois qu’une page est chargée.

Pour plus d’informations sur le suivi des événements, voir [Suivi des événements](../fundamentals/tracking-events.md).

## Étapes suivantes

Une fois les données circulées, vous pouvez effectuer les opérations suivantes.

- [Construisez votre schéma](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/schema/composition.html)
- [En savoir plus sur le débogage](../fundamentals/debugging.md)
- Découvrez comment [personnaliser l’expérience](../fundamentals/rendering-personalization-content.md)
- Découvrez comment envoyer des données à plusieurs solutions
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
