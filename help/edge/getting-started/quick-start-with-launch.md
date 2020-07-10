---
title: Démarrage rapide avec Launch
seo-title: 'SDK Web d’Adobe Experience Platform : démarrage rapide avec Launch'
description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
seo-description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
translation-type: tm+mt
source-git-commit: 9b8bddf39301cdc39bfa5370ef98d99434fc64f8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 26%

---


# Bienvenue

Ce guide décrit les différentes étapes de la configuration du SDK Web Adobe Experience Platform dans Adobe Launch. Vous devez disposer d’autorisations et être sur la liste autorisée pour utiliser cette fonctionnalité. Si vous souhaitez monter sur la liste d&#39;attente, veuillez contacter votre CSM. De plus, pour utiliser cette fonctionnalité, vous devez :

- Vous devez disposer d’un [domaine propriétaire (CNAME)](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html) activé. Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionneront sans CNAME, mais vous en aurez besoin avant de passer en production
- Vous devez utiliser la dernière version du service d’identifiant visiteur

## Création d’un ID de configuration

Vous pouvez créer un ID de configuration à l’aide de l’outil [de configuration](../fundamentals/edge-configuration.md) Edge dans Adobe Launch. Cela vous permettra de permettre au réseau Edge d&#39;envoyer des données aux différentes solutions. Consultez la page Outil [de configuration](../fundamentals/edge-configuration.md) Edge pour plus d’informations sur la manière de trouver chaque option.

>[!NOTE]
>
>Votre organisation doit être sur la liste autorisée de la fonction. Veuillez contacter votre CSM pour être ajouté à la liste autorisée.

## Préparation d’un Schéma

L&#39;Experience Platform Edge Network prend les données au format XDM. XDM est un format de données qui vous permet de définir des schémas. Le schéma définit comment le réseau Edge prévoit que les données seront formatées. Pour envoyer des données, vous devez définir votre schéma. Veillez à effectuer les opérations suivantes :

- [Création d’un schéma](../../xdm/tutorials/create-schema-ui.md)
- Ajoutez le mixin du SDK Web d’Adobe Experience Platform au schéma créé.

La vidéo suivante est destinée à vous aider à créer un schéma, un jeu de données et un connecteur source de flux continu pour vos données de SDK Web.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Installation du SDK dans Adobe Launch

Log in to Adobe Launch and install the `AEP Web SDK` extension. Dans le cadre de l’installation du SDK, vous serez invité à configurer l’extension. Saisissez l’ID de configuration que vous avez demandé ci-dessus. L’extension renseigne automatiquement l’ID d’organisation.

Pour plus d’informations sur les différentes options de configuration, voir [Configuration du SDK](../fundamentals/configuring-the-sdk.md).

## Créer une base d’éléments de données sur votre Schéma

Dans Adobe Launch, créez un élément de données qui référence le schéma en modifiant l’extension en SDK Web AEP et en définissant le type sur Objet XDM. Cela chargera votre schéma et vous permettra de mapper les éléments de données dans différentes parties du schéma.

![Elément Date de lancement](../../assets/edge_data_element.png)

## Envoi d’un événement

Une fois l’extension installée, début envoie des événements en ajoutant une action &quot;sendEvent&quot; depuis l’extension AEP Web SDK à une règle. Veillez à ajouter l’élément de données que vous venez de créer au événement en tant que données XDM. Nous vous recommandons d&#39;envoyer au moins un événement chaque fois qu&#39;une page est chargée.

Pour plus d’informations sur le suivi des événements, voir [Suivi des événements](../fundamentals/tracking-events.md).

## Étapes suivantes

Une fois que vous disposez de données, vous pouvez effectuer les opérations suivantes :

- [Construisez votre schéma](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/schema/composition.html)
- [En savoir plus sur le débogage](../fundamentals/debugging.md)
- Découvrez comment [personnaliser l’expérience](../fundamentals/rendering-personalization-content.md)
- Découvrez comment envoyer des données à plusieurs solutions
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
