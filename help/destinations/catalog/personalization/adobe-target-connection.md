---
keywords: personnalisation cible;destination;destination cible Experience Platform;destination Adobe Target;
title: Connexion Adobe Target
description: Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: f97b667f8d4dc311683b018bb1c1792aae871648
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 59%

---

# Connexion Adobe Target {#adobe-target-connection}

## Journal des modifications de destination {#changelog}

>[!IMPORTANT]
>
>Avec la version bêta du connecteur de destination Adobe Target V2 amélioré, il se peut que deux cartes Adobe Target apparaissent dans le catalogue des destinations.
>Le connecteur de destination Adobe Target V2 est actuellement en version bêta et disponible uniquement pour un nombre restreint de clients. Outre la fonctionnalité de la carte Adobe V1, le connecteur Target V2 ajoute une [étape de mappage](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) au workflow d’activation, qui vous permet de mapper les attributs de profil à Adobe Target, en activant la personnalisation basée sur les attributs de la même page et de la page suivante.

![Image des deux cartes de destination Adobe Target dans une vue côte à côte.](/help/destinations/assets/catalog/personalization/adobe-target-connection/adobe-target-side-by-side-view.png)

## Présentation {#overview}

Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc.

Adobe Target est une connexion de personnalisation dans le catalogue des destinations Adobe Experience Platform.

## Conditions préalables {#prerequisites}

### Identifiant du flux de données {#datastream-id}

Lors de la configuration de la connexion Adobe Target à [utilisation d’un identifiant de flux de données](#parameters), vous devez avoir la variable [SDK Web Adobe Experience Platform](../../../edge/home.md) implémenté.

La configuration de la connexion Adobe Target sans utiliser d’identifiant de flux de données ne nécessite pas l’implémentation du SDK Web.

>[!IMPORTANT]
>
>Avant de créer une connexion [!DNL Adobe Target], lisez le guide sur la façon de [configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md). Ce guide vous fait parcourir toutes les étapes de configuration requises pour les cas d’utilisation de la personnalisation de la même page et de la page suivante, sur plusieurs composants Experience Platform. La personnalisation de la même page et de la page suivante nécessite l’utilisation d’un identifiant de flux de données lors de la configuration de la connexion Adobe Target.

### Conditions préalables dans Adobe Target {#prerequisites-in-adobe-target}

Dans Adobe Target, assurez-vous que votre utilisateur dispose des éléments suivants :

* L’accès au [espace de travail par défaut](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* Le **Approbateur** [rôle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

En savoir plus sur l’octroi d’autorisations pour [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) et [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!DNL Profile request]** | Vous demandez tous les segments mappés dans la destination Adobe Target pour un seul profil. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas dʼutilisation {#use-cases}

**Personnaliser une bannière de page d’accueil**

Une société de location et de vente d’habitations souhaite personnaliser sa page d’accueil avec une bannière, en fonction des qualifications de segment client dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les envoyer à Adobe Target en tant que critères de ciblage pour son offre Target.

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="À propos des identifiants de flux de données"
>abstract="Cette option détermine dans quel train de données de collecte de données les segments seront inclus. Le menu déroulant affiche uniquement les trains de données pour lesquels la configuration cible est activée. Pour utiliser la segmentation Edge, vous devez sélectionner un identifiant de train de données. Si vous sélectionnez Aucun, tous les cas d&#39;utilisation qui utilisent la segmentation Edge sont désactivés."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters?lang=fr" text="En savoir plus sur la sélection des trains de données"

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Experience Platform se connecte automatiquement à l’instance Adobe Target de votre entreprise. Aucune authentification n’est requise.

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **Identifiant du flux de données**: Cela détermine dans quel flux de données de collecte de données les segments seront inclus. Le menu déroulant affiche uniquement les flux de données pour lesquels les services Target et Adobe Experience Platform sont activés. Voir [configuration d’un flux de données](../../../edge/datastreams/configure.md#aep) pour obtenir des informations détaillées sur la configuration d’un flux de données pour Adobe Experience Platform et Adobe Target.
   * **[!UICONTROL Aucun]**: Sélectionnez cette option si vous devez configurer la personnalisation Adobe Target mais que vous ne pouvez pas mettre en oeuvre le [SDK Web Experience Platform](../../../edge/home.md). Lorsque vous utilisez cette option, les segments exportés d’Experience Platform vers Target ne prennent en charge que la personnalisation de la prochaine session et la segmentation Edge est désactivée. Pour plus d’informations, consultez le tableau ci-dessous.

| Aucun flux de données sélectionné | Envoi de données sélectionné |
|---|---|
| <ul><li>[Segmentation Edge](../../../segmentation/ui/edge-segmentation.md) n’est pas prise en charge.</li><li>[Personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md) ne sont pas prises en charge.</li><li>Vous ne pouvez partager des segments avec la connexion Adobe Target que pour la variable *environnement de test de production par défaut*.</li><li>Pour configurer la personnalisation de la prochaine session sans utiliser d’identifiant de flux de données, utilisez [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>La segmentation Edge fonctionne comme prévu.</li><li>[Personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md) sont prises en charge.</li><li>Le partage de segment est pris en charge pour d’autres environnements de test.</li></ul> |

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez la section [Activer des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Adobe Target lit les données de profil du réseau Adobe Experience Platform Edge, de sorte qu’aucune donnée ne soit exportée.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).
