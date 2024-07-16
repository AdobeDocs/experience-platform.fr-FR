---
title: Connexion au moteur
description: Moengage est une plateforme d’engagement client qui optimise les interactions centrées sur les clients entre les consommateurs et les marques en temps réel.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 38%

---

# Connexion [!DNL Moengage]

## Présentation {#overview}

Utilisez la destination [!DNL Moengage] pour connecter et mapper vos données d’Adobe (attributs utilisateur, segments et événements) à MoEngage en temps réel. Les clients et clientes peuvent alors agir sur ces données, en proposant des expériences ciblées et personnalisées.

Avec l’Adobe, l’intégration est très simple et intuitive. Il vous suffit de prendre n’importe quel profil utilisateur d’Adobe et de le mapper à un attribut utilisateur MoEngage.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *Moengage*. Pour toute demande ou information, contactez directement l’équipe d’Amazon Ads à l’adresse *`https://help.moengage.com/hc/en-us`.*

## Cas d’utilisation {#use-cases}

Un marketeur souhaite cibler un segment d’utilisateurs (intégré à Adobe Experience Platform) via des campagnes [!DNL Moengage]. Ils souhaitent également personnaliser le contenu d’une campagne en fonction des attributs des profils Adobe Experience Platform. Avec cette intégration, les utilisateurs et les attributs sont mis à jour dans MoEngage dès que les segments et les profils sont mis à jour dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Avant d’envoyer vos données Adobe Experience Platform à [!DNL Moengage], notez les conditions préalables suivantes :

* Pour utiliser la destination MoEngage avec Adobe Experience Platform, les utilisateurs doivent d’abord avoir accès à leur compte [!DNL Moengage]. Consultez la page suivante pour vous inscrire ou vous connecter à votre compte MoEngage : https://app.moengage.com


## Identités prises en charge {#supported-identities}

[!DNL Moengage] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Identifiant unique qui identifie de manière unique un profil utilisateur dans le système [!DNL Moengage]. | Cet identifiant prend en charge le type de chaîne. L’un des ID utilisateur ou anonymous_id est requis. |
| anonymous_id | Un autre identifiant pour un profil utilisateur inconnu, c’est-à-dire un profil qui n’existe pas dans le système. | Cet identifiant prend en charge le type de chaîne. L’un des ID utilisateur ou anonymous_id est requis. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (user_id, anonymous_id) ainsi que les attributs personnalisés définis par vous avez exportés vers [!DNL Moengage]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Authentification de destination Moengage](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Authentification de destination Moengage](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL NOM D’UTILISATEUR]** : ID DE L’APPLICATION DE DONNÉES de la page des paramètres du tableau de bord [!DNL Moengage].
* **[!UICONTROL MOT DE PASSE]** : CLÉ DE L’APPLICATION DE DONNÉES à partir de la page des paramètres du tableau de bord [!DNL Moengage].

![Authentification de destination Moengage](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Région]** : votre application *centre de données*.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Pour envoyer correctement les données d’audience de [!DNL Adobe Experience Platform] vers la destination [!DNL Moengage], vous devez passer par l’étape de mappage des champs.

Le mappage consiste à créer un lien entre vos champs de schéma [!DNL Experience Data Model] (XDM) dans votre compte [!DNL Platform] et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL Moengage], procédez comme suit :

À l’étape [!UICONTROL Mapping], sélectionnez **[!UICONTROL Case à cocher]**.

![Mappage d’ajout de destination Moengage](../../assets/catalog/mobile-engagement/moengage/segments.png)

À l’étape [!UICONTROL Mapping], sélectionnez **[!UICONTROL Ajouter un nouveau mapping]**.

![Mappage d’ajout de destination Moengage](../../assets/catalog/mobile-engagement/moengage/mapping.png)

Dans la section [!UICONTROL Champ Source] , sélectionnez la flèche en regard du champ vide.

![Mappage du Source de destination Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ source] , vous pouvez choisir entre deux catégories de champs XDM :
* [!UICONTROL Sélectionner des attributs] : utilisez cette option pour mapper un champ spécifique de votre schéma XDM à l’attribut [!DNL Moengage].

![Attribut Source de mappage de destinations Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Sélectionnez votre champ source, puis **[!UICONTROL Sélectionner]**.

Dans la section [!UICONTROL Champ cible] , sélectionnez l’icône de mappage à droite du champ.

![Mappage de la cible de destination Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ cible] , vous pouvez choisir entre deux catégories de champs cibles :
* [!UICONTROL Sélectionner l’espace de noms d’identité] : utilisez cette option pour mapper les espaces de noms d’identité [!DNL Platform] aux espaces de noms d’identité [!DNL Moengage].
* [!UICONTROL Sélectionner des attributs personnalisés] : utilisez cette option pour mapper des attributs XDM aux attributs [!DNL Moengage] personnalisés que vous avez définis dans votre compte [!DNL Moengage]. <br> Vous pouvez également utiliser cette option pour renommer les attributs XDM existants en [!DNL Moengage]. Par exemple, le mappage d’un attribut XDM `lastName` à un attribut `Last_Name` personnalisé dans [!DNL Moengage], créera l’attribut `Last_Name` dans [!DNL Moengage], s’il n’existe pas déjà, et lui mappera l’attribut XDM `lastName`.

![Champs de mappage de la cible de destination Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Sélectionnez votre champ cible, puis **[!UICONTROL Sélectionner]**.

Vous devriez maintenant voir votre mappage de champ dans la liste.

![Mappage de destination Moengage Complete](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Pour ajouter d’autres mappages, répétez les étapes précédentes.

## Données exportées / Valider l’exportation des données {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Moengage], accédez au profil utilisateur de votre compte [!DNL Moengage]. Un attribut d’utilisateur appelé Segment AEP s’affiche.

![Mappage de destination Moengage Complete](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
