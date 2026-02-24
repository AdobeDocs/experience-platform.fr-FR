---
title: Échange d'index
description: Connectez-vous à Index Exchange (Index) et activez vos données afin que vos segments d’audience puissent être ciblés par les offres créées dans l’interface utilisateur d’Index.
last-substantial-update: 2026-01-27T00:00:00Z
exl-id: 6d2a8553-5e8c-4eeb-ac25-5e4c2bdc5758
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 15%

---

# [!DNL Index Exchange] {#index-exchange}

## Vue d’ensemble {#overview}

[!DNL Index] est une plateforme publicitaire mondiale axée sur l’offre qui aide les propriétaires de médias à maximiser la valeur de leur contenu sur chaque écran. Fort de plus de 20 ans de leadership dans le secteur, [!DNL Index] met en relation les plus grandes marques du monde avec des créateurs d’expériences haut de gamme afin de proposer des expériences client de haute qualité.

Utilisez ce connecteur de destination pour exporter des segments d’audience de Adobe Experience Platform directement vers la plateforme de publicité programmatique d’[!DNL Index Exchange].

Une fois exportés, ces segments d’audience peuvent être utilisés pour cibler les offres des propriétaires de médias, des partenaires de marketplace, ou partagés avec les éditeurs et les conservateurs par les fournisseurs de marketplace.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Index]. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse [technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Index Exchange], consultez les exemples de cas d’utilisation ci-dessous que la clientèle Experience Platform peut résoudre.

### Ciblage des utilisateurs sur les plateformes mobiles, web et CTV {#targeting-users}

Propriétaires de médias, partenaires de marketplace ou fournisseurs de marketplace qui souhaitent envoyer des audiences d&#39;Experience Platform vers [!DNL Index] pour cibler les utilisateurs sur les plateformes mobiles, web et CTV, en utilisant un large éventail d&#39;identifiants.

### Ciblage de contenu spécifique sur des plateformes mobiles, web et CTV {#targeting-content}

Les propriétaires de médias, les partenaires de marketplace ou les fournisseurs de marketplace qui souhaitent envoyer des audiences d&#39;Experience Platform vers [!DNL Index] à cibler les utilisateurs qui recherchent un contenu spécifique sur des plateformes mobiles, web et CTV à l&#39;aide d&#39;URL spécifiques, d&#39;App Bundles ou d&#39;ID de contenu.

## Conditions préalables {#prerequisites}

Les segments d’audience doivent être enregistrés auprès de [!DNL Index] à l’aide d’un processus supplémentaire lors de l’utilisation de cette destination avant d’apparaître dans votre compte. Contactez votre représentant de compte [!DNL Index Exchange] pour obtenir de l’aide sur ce processus.

## Identités prises en charge {#supported-identities}

[!DNL Index] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Notez que les destinations [!DNL Index Exchange] ne prennent en charge qu’un seul type d’identité par chargement. Vous devez spécifier le type d’identifiant approprié lors de la configuration des détails de destination (voir la section [« Renseigner les détails de destination »](#destination-details) ci-dessous).

Pour charger plusieurs types d’identité, créez des instances distinctes de la destination [!DNL Index Exchange] pour chaque type d’identité.

| Identité cible | Description | Considérations |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | Si l’identité source est un espace de noms GAID, sélectionnez GAID comme identité cible. |
| IDFA | Identifiant Apple pour les annonceurs | Si votre identité source est un espace de noms IDFA, sélectionnez l’identité cible IDFA. |
| Windows AID | ID Windows Advertising | Si votre identité source est un espace de noms d’assistance Windows, sélectionnez l’identité cible de l’assistance Windows. |
| extern_id | ID d’utilisateur personnalisés | Si votre identité source est un espace de noms personnalisé, sélectionnez cette identité cible. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section explique les types d’audience que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
| --------- | ---------- | ---------- |
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
| --------- | ---------- | --------- | 
| Type d’exportation | **[!UICONTROL Segment export]** | Exporte tous les membres d’un segment (audience) ainsi que les identifiants (IDFA, GAID ou autres) utilisés dans la destination [!DNL Index Exchange]. |
| Fréquence des exportations | **[!UICONTROL Batch]** | Exporte des fichiers vers des plateformes en aval à intervalles de 3, 6, 8, 12 ou 24 heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détails de la destination](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name] : saisissez un nom pour vous aider à reconnaître cette destination ultérieurement.
* [!UICONTROL Description] : saisissez une description pour vous aider à identifier cette destination ultérieurement.
* [!UICONTROL Identifier Type] : sélectionnez le type d’identifiant fourni par l’index qui correspond à l’identifiant que vous envoyez à [!DNL Index]. Consultez le tableau des types d’identifiants pris en charge ci-dessous. Si vous ne savez pas quel type d’identifiant utiliser, contactez votre représentant [!DNL Index]. Pour envoyer plusieurs types d’identifiants, créez des instances distinctes de cette destination.
* [!UICONTROL Account ID] : saisissez votre ID de compte [!DNL Index]. Il ne s’agit pas du même que votre ID d’éditeur. Si vous n’êtes pas sûr de l’ID à utiliser, contactez votre représentant [!DNL Index].

#### Types d’identifiants pris en charge

| Type d’identifiant | Description |
|------------------ | ------------- |
| [!DNL appbundle] | Offre groupée d’applications mobiles |
| [!DNL contentid] | Identifiant du contenu |
| [!DNL deviceid] | Identifiant de l’appareil (par exemple, IDFA, GAID, WAID, etc.) |
| [!DNL ip] | Adresse IP |
| [!DNL postcode] | Code postal |
| [!DNL url] | URL du site |
| [!DNL ppid_xxx] | Pour les identifiants PPID, contactez votre représentant de compte [!DNL Index Exchange] pour obtenir de l’aide. |

{style="table-layout:auto"}

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers cette destination. Sélectionnez une ou plusieurs alertes dans la liste pour vous abonner aux notifications de statut de votre flux de données. Pour plus d’informations, consultez le guide sur [l’abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).
Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Sélection des champs sources :

* Sélectionnez un identifiant (généralement des espaces de noms tels qu’IDFA ou un espace de noms d’identifiant personnalisé). Il doit correspondre au Type d’identifiant sélectionné lors de la configuration de la destination. Par exemple, lors de l’utilisation de l’identifiant IDFA comme champ source, la destination doit avoir été configurée avec le type d’identifiant « deviceid ».

Sélection des champs cibles :

* Les noms des champs cibles sont ignorés et ne sont pas importants. La destination ne se soucie que du type d’identifiant envoyé, qui est déterminé par le Type d’identifiant sélectionné lors de la configuration de la destination.

![Mappage des attributs et des identités](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### Enregistrement des segments avec [!DNL Index] {#register-segments}

Avant ou après l’activation des données vers la destination, contactez votre représentant [!DNL Index] pour enregistrer les segments que vous prévoyez d’activer. Votre représentant vous fournira des instructions sur la manière d’enregistrer des détails de segment supplémentaires, y compris les noms, identifiants, descriptions et prix, le cas échéant.

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois l’enregistrement terminé, les segments seront disponibles pour le ciblage dans votre compte [!DNL Index]. Pour confirmer que les données sont correctement reçues, contactez votre représentant [!DNL Index], qui peut fournir des détails sur le volume de données de segment reçues.

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations Experience Platform sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont Experience Platform applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
