---
title: Connexion Google Ads
description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises de faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 64%

---

# Connexion [!DNL Google Ads]

## Vue d’ensemble {#overview}

[!DNL Google Ads], appelé auparavant [!DNL Google AdWords], est un service de publicité en ligne qui permet aux entreprises de faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos [!DNL YouTube] et des affichages mobiles in-app.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Ads] :

* Les audiences activées sont créées par programmation dans la plateforme [!DNL Google].
* [!DNL Experience Platform] n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Google Ads] sans jamais avoir activé la fonctionnalité de synchronisation des identifiants [ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service Experience Cloud ID par le passé (avec Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations Google dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Experience Platform.

## Identités prises en charge {#supported-identities}

[!DNL Google Ads] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=fr), également appelé [!DNL Device ID]. Identifiant numérique à 38 chiffres associé par Audience Manager à chaque appareil avec lequel il interagit. | Google utilise [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=fr) pour cibler les utilisateurs en Californie et l’ID de cookie Google pour tous les autres utilisateurs. |
| ID de cookie [!DNL Google] | ID de cookie [!DNL Google] | [!DNL Google] utilise cet identifiant pour cibler les utilisateurs situés en dehors de la Californie. |
| RIDA | ID Roku pour la publicité. Cet identifiant identifie de manière unique les appareils Roku. |  |
| MAID | ID Microsoft Advertising. Cet identifiant identifie de manière unique les appareils exécutant Windows 10. |  |
| ID Amazon Fire TV | Cet identifiant identifie de manière unique les téléviseurs Amazon Fire. |  |

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
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez toutes les personnes membres d’une audience vers la destination Google. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

### Compte [!DNL Google Ads] existant

>[!IMPORTANT]
>
> [!DNL Google] a abandonné les nouvelles intégrations de cookies [!DNL Google Ads] avec des fournisseurs tiers. Pour effectuer les étapes de placé sur la liste autorisée de la section suivante, vous devez disposer d’une intégration existante à [!DNL Google Ads]. Par conséquent, l’approche recommandée pour l’utilisation de [!DNL Google Ads] est de configurer une intégration [!DNL Google Customer Match]. Pour plus d’informations sur la création d’une intégration [!DNL Google Customer Match], consultez le tutoriel sur la création d’une connexion [[!DNL Google Customer Match]](./google-customer-match.md).

### Liste autorisée {#allow-listing}

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ads] dans Experience Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.
>Une exception à cette règle s’applique aux clients d’[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=fr). Si vous avez déjà créé une connexion à cette destination Google dans Audience Manager, il n’est pas nécessaire de passer à nouveau par le processus de liste autorisée et vous pouvez passer directement aux étapes suivantes.

Avant de créer la destination [!DNL Google Ads] dans Experience Platform, vous devez contacter [!DNL Google] pour qu’Adobe soit placé sur la liste des fournisseurs de données autorisés et pour que votre compte soit ajouté à la place sur la liste autorisée. Contactez [!DNL Google] et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte Adobe avec Google. Identifiant de compte : 87933855.
* **Identifiant client** : l’identifiant client d’Adobe avec Google. Identifiant client : 89690775.
* Votre type de compte : **AdWords**
* **Identifiant Google AdWords** : il s’agit de votre identifiant avec [!DNL Google]. Le format d’identifiant est généralement 123-456-7890.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Account Type]** : AdWords est la seule option disponible.
* **[!UICONTROL Account ID]** : renseignez votre identifiant de compte avec [!DNL Google Ads]. Le format d’identifiant est généralement 123-456-7890.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Ads], vérifiez votre compte [!DNL Google Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.

## Résolution des problèmes {#troubleshooting}

### Message d’erreur 400 Requête incorrecte {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les comptes clients ne respectent pas les [conditions préalables](#prerequisites) ou lorsque les clientes et clients tentent de configurer la destination sans un compte [!DNL Google Ads] existant.

[!DNL Google] a abandonné les nouvelles intégrations de cookies [!DNL Google Ads] avec des fournisseurs tiers. Pour effectuer les étapes de [place sur la liste autorisée ](#allow-listing), vous devez disposer d&#39;une intégration existante avec [!DNL Google Ads].

L’approche recommandée pour l’utilisation de [!DNL Google Ads] est de configurer une intégration [[!DNL Google Customer Match]](google-customer-match.md).
