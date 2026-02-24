---
title: Connexion Liste des Clients Pinterest
description: Créez des audiences à partir de vos listes de clients, des personnes qui ont visité votre site ou de celles qui ont déjà interagi avec votre contenu sur Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 29%

---

# Connexion [!DNL Pinterest Customer List]

## Vue d’ensemble {#overview}

Créez des audiences à partir de vos listes de clients, des personnes qui ont visité votre site ou de celles qui ont déjà interagi avec votre contenu sur Pinterest.

>[!IMPORTANT]
>
>Cette destination a été créée par l’équipe Pinterest. Pour toute demande ou information, contactez directement l&#39;équipe à l&#39;adresse https://help.pinterest.com/en/contact.

## Conditions préalables {#prerequisites}

* L’utilisateur doit s’authentifier avec un compte Pinterest ayant accès au compte de l’annonceur auquel il souhaite ajouter une audience. Vous trouverez des détails sur le partage de comptes d’annonceurs [ici](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Plus précisément, l’utilisateur ou l’utilisatrice aurait besoin des niveaux d’accès « audience ».
* Vous trouverez des détails sur les formats d’identité de liste de clients [ici](https://help.pinterest.com/en/business/article/audience-targeting).

## Identités prises en charge {#supported-identities}

La destination [!DNL Pinterest Customer List] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

Dans l’étape [mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, mappez les identités souhaitées au champ cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion des données dans Pinterest.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mappez l’espace de noms d’identité source *GAID* au champ d’identité cible *pinterest_audience*. |
| IDFA | [!DNL Apple ID for Advertisers] | Mappez l’espace de noms d’identité source *IDFA* au champ d’identité cible *pinterest_audience*. |
| EMAIL | Adresses e-mail (texte clair ou haché avec l’algorithme SHA256) | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. <br> Mappez l’espace de noms d’identité source *Email* ou *Email_LC_SHA256* au champ d’identité cible *pinterest_audience*. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Liste de clients Pinterest . |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Pinterest Customer List], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation 1

Créez des audiences à partir de vos listes de clients, des personnes qui ont visité votre site ou de celles qui ont déjà interagi avec votre contenu sur Pinterest.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Ad Account ID]** : votre ID d’annonceur Pinterest.

### Actualiser les informations d’identification d’authentification {#refresh-authentication-credentials}

Les jetons Pinterest expirent tous les 30 jours. Vous pouvez surveiller les dates d’expiration de votre jeton à partir de la colonne **[!UICONTROL Account expiration date]** dans les onglets **[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)** .

Une fois le jeton expiré, les exportations de données vers la destination cessent de fonctionner. Pour éviter cette situation, réauthentifiez-vous en procédant comme suit :

1. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. (Facultatif) Utilisez les filtres disponibles sur la page pour afficher uniquement les comptes Pinterest.
   ![Filtrer pour afficher uniquement les comptes Pinterest](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. Sélectionnez le compte à actualiser, puis les points de suspension et sélectionnez **[!UICONTROL Edit details]**.
   ![Sélectionnez Modifier les détails](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png)
4. Dans la fenêtre modale, sélectionnez **[!UICONTROL Reconnect OAuth]** et réauthentifiez-vous à l’aide de vos informations d’identification Pinterest.
   ![Fenêtre modale avec l’option Reconnecter OAuth &#x200B;](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Vos informations d’authentification sont actualisées et leur délai d’expiration est réinitialisé à 30 jours.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Reportez-vous à la page Centre d&#39;aide de [Pinterest](https://help.pinterest.com/en/business/article/audience-targeting) pour plus d&#39;informations.

+++ Afficher le journal des modifications


| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Novembre 2023 | Nouvelles fonctionnalités et mise à jour de la documentation | La destination Pinterest dans Real-Time CDP utilise désormais l’API publicitaire v5. |

{style="table-layout:auto"}


+++
