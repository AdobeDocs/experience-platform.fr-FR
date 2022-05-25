---
keywords: personnalisation cible;destination;destination cible Experience Platform;destination Adobe Target;
title: Connexion Adobe Target
description: Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 0868d81bcd1968b3223c79abb5a7bb8f279a4130
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 45%

---

# Connexion Adobe Target {#adobe-target-connection}

## Présentation {#overview}

Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc.

Adobe Target est une connexion de personnalisation dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Lors de la configuration de la connexion Adobe Target à [utilisation d’un identifiant de flux de données](#parameters), vous devez avoir la variable [SDK Web Adobe Experience Platform](../../../edge/home.md) implémenté.

La configuration de la connexion Adobe Target sans utiliser d’identifiant de flux de données ne nécessite pas l’implémentation du SDK Web.

>[!IMPORTANT]
>
>Avant de créer une connexion [!DNL Adobe Target], lisez le guide sur la façon de [configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md). Ce guide vous fait parcourir toutes les étapes de configuration requises pour les cas d’utilisation de la personnalisation de la même page et de la page suivante, sur plusieurs composants Experience Platform. La personnalisation de la même page et de la page suivante nécessite l’utilisation d’un identifiant de flux de données lors de la configuration de la connexion Adobe Target.

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!DNL Profile request]** | Vous demandez tous les segments mappés dans la destination Adobe Target pour un seul profil. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Cas dʼutilisation {#use-cases}

**Personnaliser une bannière de page d’accueil**

Une société de location et de vente d’habitations souhaite personnaliser sa page d’accueil avec une bannière, en fonction des qualifications de segment client dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les envoyer à Adobe Target en tant que critères de ciblage pour son offre Target.

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="À propos des identifiants de flux de données"
>abstract="Cette option détermine dans quel jeu de données de collecte de données les segments seront inclus. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration Target est activée. Pour utiliser la segmentation Edge, vous devez sélectionner un identifiant de flux de données. Si vous sélectionnez Aucun, tous les cas d’utilisation qui utilisent la segmentation Edge sont désactivés."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="En savoir plus sur la sélection des flux de données."

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Experience Platform se connecte automatiquement à l’instance Adobe Target de votre entreprise. Aucune authentification n’est requise.

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **Identifiant du flux de données**: Cela détermine dans quel flux de données de collecte de données les segments seront inclus. Le menu déroulant affiche uniquement les flux de données pour lesquels la destination Target est activée. Voir [configuration d’un flux de données](../../../edge/datastreams/overview.md#target) pour obtenir des informations détaillées sur la configuration d’un flux de données pour Adobe Target.
   * **[!UICONTROL Aucun]**: Sélectionnez cette option si vous devez configurer la personnalisation Adobe Target mais que vous ne pouvez pas mettre en oeuvre le [SDK Web Experience Platform](../../../edge/home.md). Lorsque vous utilisez cette option, les segments exportés d’Experience Platform vers Target ne prennent en charge que la personnalisation de la prochaine session et la segmentation Edge est désactivée. Pour plus d’informations, consultez le tableau ci-dessous.

| Aucun flux de données sélectionné | Envoi de données sélectionné |
|---|---|
| <ul><li>[Segmentation Edge](../../../segmentation/ui/edge-segmentation.md) n’est pas prise en charge.</li><li>[Personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md) ne sont pas prises en charge.</li><li>Vous pouvez partager des segments sur la connexion Adobe Target uniquement pour l’environnement de test de production.</li><li>Pour configurer la personnalisation de la prochaine session sans utiliser d’identifiant de flux de données, utilisez [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>La segmentation Edge fonctionne comme prévu.</li><li>[Personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md) sont prises en charge.</li><li>Le partage de segment est pris en charge pour d’autres environnements de test.</li></ul> |

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez la section [Activer des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Adobe Target lit les données de profil du réseau Adobe Experience Platform Edge, de sorte qu’aucune donnée ne soit exportée.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).
