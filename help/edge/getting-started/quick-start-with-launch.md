---
title: Démarrage rapide avec Launch
seo-title: 'SDK Web d’Adobe Experience Platform : démarrage rapide avec Launch'
description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
seo-description: Guide de démarrage rapide pour utiliser l’extension SDK Web d’Experience Platform pour la collecte de données
translation-type: tm+mt
source-git-commit: 62b18ed8f70ad87b04f60ade5730ff30d8985415
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 32%

---


# Bienvenue

Ce guide décrit les différentes étapes de la configuration du SDK Web d’Adobe Experience Platform au lancement. Pour pouvoir utiliser cette fonctionnalité, vous devez disposer d’autorisations et être sur la liste autorisée. Si vous souhaitez monter sur la liste d&#39;attente, veuillez vous adresser à votre CSM.

- Vous devez disposer d’un [domaine propriétaire (CNAME)](https://docs.adobe.com/content/help/fr-FR/core-services/interface/ec-cookies/cookies-first-party.html) activé. Si vous disposez déjà d’un CNAME pour Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionneront sans CNAME, mais vous en aurez besoin avant de passer en production
- Vous devez utiliser la dernière version du service d’identifiant visiteur

## Création d’un ID de configuration

Vous pouvez créer un ID de configuration à l’aide de l’outil [de configuration](../fundamentals/edge-configuration.md) edge au lancement. Cela vous permettra de permettre au réseau Edge d&#39;envoyer des données aux différentes solutions. Vous trouverez des informations détaillées sur la manière de trouver chaque option dans la page Outil [de configuration](../fundamentals/edge-configuration.md) Edge.

>[!NOTE]
>
>Votre organisation doit se trouver sur la liste autorisée de la fonction. Veuillez contacter votre CSM pour être mis sur la liste autorisée.

## Préparation d’un Schéma

Le réseau Edge de plate-forme d’expérience prend les données au format XDM. XDM est un format de données qui vous permet de définir des schémas. Le schéma définit comment le réseau Edge prévoit que les données seront formatées. Pour envoyer des données, vous devez définir votre schéma.

- [Création d’un schéma](../../xdm/tutorials/create-schema-ui.md)
- Ajoutez le mixin du SDK Web d’Adobe Experience Platform au schéma créé.

## Installation du SDK dans Launch

Connectez-vous à Launch et installez l’extension `AEP Web SDK`. Dans le cadre de l’installation du SDK, vous serez invité à configurer l’extension. Entrez l’ID de configuration que vous avez demandé ci-dessus. L’extension renseigne automatiquement l’ID d’organisation.

Pour plus d’informations sur les différentes options de configuration, voir [Configuration du SDK](../fundamentals/configuring-the-sdk.md).

## Créer une base d’éléments de données sur votre Schéma

Au lancement, créez un élément de données qui référence le schéma en modifiant l’extension en SDK Web AEP et en définissant le type sur Objet XDM. Cela chargera votre schéma et vous permettra de mapper les éléments de données dans différentes parties du schéma.

![Elément Date de lancement](../../assets/edge_data_element.png)

## Envoi d’un événement

Une fois l’extension installée, début envoie des événements en ajoutant une action &quot;sendEvent&quot; depuis l’extension AEP Web SDK à une règle. Veillez à ajouter l’élément de données que vous venez de créer au événement en tant que données XDM. Nous vous recommandons d&#39;envoyer au moins un événement chaque fois qu&#39;une page est chargée.

Pour plus d’informations sur le suivi des événements, voir [Suivi des événements](../fundamentals/tracking-events.md).

## Étapes suivantes

Une fois que vous disposez de données, vous pouvez effectuer les opérations suivantes.

- [Construisez votre schéma](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [En savoir plus sur le débogage](../fundamentals/debugging.md)
- Découvrez comment [personnaliser l’expérience](../fundamentals/rendering-personalization-content.md)
- Découvrez comment envoyer des données à plusieurs solutions
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
