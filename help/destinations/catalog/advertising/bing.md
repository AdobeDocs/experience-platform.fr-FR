---
keywords: 'publicité ; bing; '
title: Destination Microsoft Bing
seo-title: La destination Microsoft Bing vous aide à envoyer des données de profil à Microsoft Display Advertising.
description: Avec la destination Microsoft Bing, vous pouvez exécuter des campagnes numériques ciblées de reciblage et d'audience sur l'ensemble des campagnes Microsoft Display Advertising.
seo-description: Avec la destination Microsoft Bing, vous pouvez exécuter des campagnes numériques ciblées de reciblage et d'audience sur l'ensemble des campagnes Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 6%

---


# [!DNL Microsoft Bing] destination

## Présentation {#overview}

La destination [!DNL Microsoft Bing] vous aide à envoyer des données de profil à [!DNL Microsoft Display Advertising].

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d&#39;abord vous connecter à la destination.

## Spécifications de la destination {#destination-specs}

Notez les détails suivants spécifiques à la destination [!DNL Microsoft Bing] :

* Vous pouvez envoyer les [identités](../../../identity-service/namespaces.md) suivantes à [!DNL Microsoft Bing] destinations : [!DNL Microsoft ID].

## Cas d’utilisation {#use-cases}

En tant que spécialiste du marketing, je souhaite pouvoir utiliser des segments créés à partir de [!DNL Microsoft Advertising IDs] pour les utilisateurs de cible par le biais de publicités affichées sur [!DNL Microsoft Advertising] canaux.

## Type d&#39;exportation {#export-type}

**[!DNL Segment Export]** - vous exportez tous les membres d&#39;un segment (audience) vers la  [!DNL Microsoft Bing] destination.

## Conditions préalables {#prerequisites}

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL ID] du compte : il s&#39;agit de votre  [!DNL Bing Ads CID]format entier.

## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Microsoft Bing], puis **[!UICONTROL Configurer]**.

![Configuration de la destination Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.
>
>![Activer la destination Microsoft Bing](../../assets/catalog/advertising/bing/activate.png)

À l&#39;étape [!UICONTROL Authentification], vous devez saisir les détails de la connexion de destination :

* **[!UICONTROL Nom]** : Nom par lequel vous reconnaîtrez cette destination dans le futur.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination dans le futur.
* **[!UICONTROL ID]** du compte : Votre  [!DNL Bing Ads CID].
* **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation du marketing, voir la [Gouvernance des données dans Adobe Experience Platform](../../../data-governance/policies/overview.md) page. Pour plus d&#39;informations sur les cas d&#39;utilisation marketing définis par l&#39;Adobe, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

![Authentification de destination Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Cliquez sur **[!UICONTROL Créer une destination]**. Votre destination est maintenant créée. Vous pouvez cliquer sur [!UICONTROL Enregistrer et quitter] si vous souhaitez activer les segments ultérieurement, ou sur [!UICONTROL Suivant] pour poursuivre le processus et sélectionner les segments à activer. Dans les deux cas, consultez la section suivante, [Activer les segments](#activate-segments), pour le reste du flux de travail.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md#select-attributes).

À l’étape [Planification des segments](../../ui/activate-destinations.md#segment-schedule), vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la destination.

Lors du mappage de segments, nous vous recommandons d’utiliser le nom de segment [!DNL Platform] ou une forme plus courte de celui-ci, pour en faciliter l’utilisation. Cependant, l’ID ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre compte [!DNL Platform]. Toute valeur que vous insérez dans le champ de mappage est répercutée par la destination.

![ID de mappage de segments](../../assets/common/segment-mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.