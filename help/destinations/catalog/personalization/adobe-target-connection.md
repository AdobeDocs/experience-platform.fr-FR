---
keywords: personnalisation cible;destination;destination cible Experience Platform;destination Adobe Target;
title: Connexion Adobe Target
description: Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 77%

---

# Connexion Adobe Target {#adobe-target-connection}

## Présentation {#overview}

Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc.

Adobe Target est une connexion de personnalisation dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Cette intégration est optimisée par la fonction [SDK Web Adobe Experience Platform](../../../edge/home.md). Vous devez utiliser ce SDK pour utiliser cette destination.

>[!IMPORTANT]
>
>Avant de créer une connexion [!DNL Adobe Target], lisez le guide sur la façon de [configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md). Ce guide vous fait parcourir toutes les étapes de configuration requises pour les cas d’utilisation de la personnalisation de la même page et de la page suivante, sur plusieurs composants Experience Platform.

## Type d’exportation et fréquence {#export-type-frequency}

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
>abstract="Cette option détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Vous devez configurer un flux de données avant de pouvoir configurer votre destination."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr" text="Découvrez comment configurer un flux de données"

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Experience Platform se connecte automatiquement à l’instance Adobe Target de votre entreprise. Aucune authentification n’est requise.

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **Identifiant du flux de données** : détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../edge/fundamentals/datastreams.md) pour plus d’informations.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez la section [Activer des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Adobe Target lit les données de profil du réseau Adobe Experience Platform Edge, de sorte qu’aucune donnée ne soit exportée.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).
