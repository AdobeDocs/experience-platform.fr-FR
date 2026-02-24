---
title: Destination par lots Magnite
description: Utilisez cette destination pour diffuser des audiences Adobe CDP vers la plateforme de streaming Magnite par lots.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 8cc3890f-84f8-49d1-a329-322c13f9e5af
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1782'
ht-degree: 12%

---

# Magnite : connexion par lots {#magnite-streaming-batch}

## Vue d’ensemble {#overview}

Ce document décrit la destination Magnite : par lots et fournit des exemples de cas d’utilisation pour vous aider à mieux comprendre comment activer et exporter des audiences vers celle-ci.

Les audiences Adobe Real-Time CDP peuvent être diffusées sur la plateforme de streaming Magnite de deux manières : elles peuvent être diffusées une fois par jour ou en temps réel :

1. Si vous souhaitez et/ou devez uniquement diffuser des audiences une fois par jour, vous pouvez utiliser la destination Magnite : Batch , qui diffuse des audiences vers Magnite Streaming via une diffusion quotidienne de fichiers par lots S3. Ces audiences par lots sont stockées indéfiniment sur la plateforme Magnite, contrairement aux audiences en temps réel, qui ne sont stockées que pendant quelques jours.

2. Cependant, si vous souhaitez ou devez diffuser des audiences plus fréquemment, vous devez utiliser la destination [Magnite Real-Time](/help/destinations/catalog/advertising/magnite-streaming.md). Lors de l’utilisation de la destination en temps réel, Magnite Streaming recevra les audiences en temps réel, mais Magnite ne peut stocker les audiences en temps réel que temporairement dans sa plateforme et elles seront supprimées du système dans un délai de deux jours. Pour cette raison, si vous souhaitez utiliser la destination en temps réel Magnite, vous devez *également* utiliser la destination Magnite : lot . Pour chaque audience que vous activez vers la destination en temps réel, vous devez également activer vers la destination par lots .

En résumé : si vous souhaitez diffuser des audiences Adobe Real-Time CDP une seule fois par jour, vous utiliserez la destination Magnite : Batch uniquement et les audiences seront diffusées une fois par jour. Si vous souhaitez diffuser des audiences Adobe Real-Time CDP en temps réel, vous utiliserez *à la fois* la destination Magnite : par lots et la destination Magnite en temps réel. Pour plus d’informations, contactez Magnite : Streaming.


Poursuivez la lecture ci-dessous pour plus d’informations sur la destination Magnite : par lots, comment vous y connecter et comment y activer les audiences Adobe Real-Time CDP.
Pour plus d’informations sur la destination en temps réel, voir [cette page de documentation](magnite-streaming.md) à la place.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Magnite]. Pour toute demande ou information, contactez directement l’équipe d’Amazon Ads au `adobe-tech@magnite.com`.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination Magnite : Batch , consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1 {#use-case-1}

Vous avez activé une audience sur la destination en temps réel Magnite .

Toutes les audiences activées via la destination en temps réel de Magnite doivent également utiliser la destination Magnite : lot , car les données de la diffusion par lots sont destinées à remplacer/conserver les données de la diffusion en temps réel dans la plateforme de streaming Magnite.

### Cas d’utilisation #2 {#use-case-2}

Vous souhaitez activer une audience uniquement à une cadence par lots/quotidienne vers la plateforme de streaming Magnite.

Toute audience activée via la destination Magnite : lot sera diffusée à une cadence par lots/quotidienne et sera ensuite disponible pour le ciblage dans la plateforme de streaming Magnite.

## Conditions préalables {#prerequisites}

Pour utiliser les destinations [!DNL Magnite] dans Adobe Experience Platform, vous devez d’abord disposer d’un compte de streaming Magnite. Si vous disposez d’un compte [!DNL Magnite Streaming], contactez votre gestionnaire de compte [!DNL Magnite] afin d’obtenir des informations d’identification pour accéder aux destinations [!DNL Magnite's]. Si vous n’avez pas de compte [!DNL Magnite Streaming], veuillez contacter adobe-tech@magnite.com

## Identités prises en charge {#supported-identities}

La destination Magnite : lot peut recevoir *toutes* sources d’identité du CDP d’Adobe. Actuellement, cette destination comporte trois champs d’identité cible que vous pouvez mapper.

>[!NOTE]
>
>*N’importe laquelle* les sources d’identité peuvent mapper à n’importe laquelle des identités cibles `magnite_deviceId`.

| Identité cible | Description | Considérations |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| magnite_deviceId_GAID | GOOGLE ADVERTISING ID | Sélectionnez cette identité cible lorsque votre identité source est un GAID |
| magnite_deviceId_IDFA | Identifiant Apple pour les annonceurs | Sélectionner cette identité cible lorsque votre identité source est un IDFA |
| magnite_deviceId_CUSTOM | Identifiant personnalisé/défini par l’utilisateur | Sélectionnez cette identité cible lorsque votre identité source n’est pas un GAID ou un IDFA, ou s’il s’agit d’un identifiant personnalisé ou défini par l’utilisateur |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

| Origine de l’audience | Pris en charge | Description |
|-----------------------------|----------|----------|
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

| Élément | Type | Notes |
|-----------------------------|----------|----------|
| Type d’exportation | Exportation d’audience | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Magnite : lot . |
| Fréquence des exportations | Lot | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les destinations par lots [basées sur des fichiers](/help/destinations/destination-types.md). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Une fois que l’utilisation de la destination a été approuvée et que la diffusion en continu Magnite a partagé vos informations d’identification, suivez les étapes ci-dessous pour authentifier, mapper et partager des données.

### S’authentifier auprès de la destination {#authenticate}

Recherchez la destination Magnite : Batch dans le catalogue d’expériences Adobe. Cliquez sur le bouton d’options supplémentaires (\...), puis configurez la connexion/instance de destination.

Si vous disposez déjà d’un compte , vous pouvez le localiser en remplaçant l’option Type de compte par « Compte existant ». Sinon, vous allez créer un compte ci-dessous :

Pour créer un compte et l’authentifier pour la première fois auprès de la destination, renseignez les champs « Clé d’accès S3 » et « Clé secrète S3 » requis (qui vous sont fournis via votre gestionnaire de compte), puis sélectionnez **[!UICONTROL Connect to destination]**

![champs d’authentification de la configuration de destination vides](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>La politique de sécurité de Magnite Streaming nécessite une rotation régulière des clés S3. Vous devez vous attendre à mettre à jour votre compte à l’avenir avec de nouveaux accès S3 et de nouvelles clés secrètes S3. Vous n’avez qu’à mettre à jour le compte lui-même : les destinations utilisant ce compte utiliseront automatiquement les clés mises à jour. Si les nouvelles clés ne sont pas chargées, les données ne seront pas envoyées à cette destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette connexion/instance de destination dans le
future.
* **[!UICONTROL Description]** : description qui vous aidera à l’identifier
connexion/instance de destination à l’avenir.
* **[!UICONTROL Your company name]** : nom de votre client/société. Seuls les clients [!DNL Magnite Streaming] pris en charge peuvent être sélectionnés.

>[!NOTE]
>
>Le nom de la société doit être une chaîne correspondant au nom du compartiment de diffusion Amazon S3 que vous avez configuré avec Magnite et configuré à l’étape [s’authentifier à la destination](#authenticate). Les caractères pris en charge sont « a-z », « A-Z », « 0-9 », « - » (tiret) ou « _ » (trait de soulignement).

![champs d’authentification de la configuration de destination renseignés](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>Si vous prévoyez d’envoyer plusieurs types d’identifiants (GAID, IDFA, etc.) à l’aide de la destination par lots, une nouvelle connexion/instance de destination est requise pour chaque type. Veuillez contacter votre représentant de compte Magnite pour plus d’informations.

Vous pouvez ensuite procéder en sélectionnant **[!UICONTROL Next]**

Dans l’écran suivant, intitulé « Politique de gouvernance et actions d’application (facultatives) », vous pouvez éventuellement sélectionner n’importe quelle politique de gouvernance des données appropriée. « Exportation de données » est généralement sélectionné pour la destination Magnite : lot .

![Politique de gouvernance facultative et mesures d’application](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

Une fois sélectionné, ou si vous souhaitez ignorer cet écran facultatif, sélectionnez **[!UICONTROL Create]**

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

### Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Dans le **[!UICONTROL Source field]**, vous pouvez sélectionner n’importe quel attribut ou identité pour vos appareils. Dans cet exemple, nous avons sélectionné une carte des identités personnalisée appelée « DeviceId »
![mapper les champs de données souhaités au champ device_id](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

Dans le **[!UICONTROL Target field]** :
![sélectionnez l’identité cible du type d’appareil approprié](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) Consultez [Identités prises en charge](#supported-identities) pour plus d’informations.
Dans cet exemple, nous avons sélectionné le **[!UICONTROL Target field]** : magnite_deviceId_CUSTOM, car notre **[!UICONTROL Source field]** a été défini comme un IdentityMap personnalisé : DeviceID.

>[!NOTE]
>
>Si vous prévoyez d’envoyer/mapper plusieurs types d’ID (GAID, IDFA, etc.) à l’aide de la destination par lots, une nouvelle connexion/instance de destination est requise pour chaque. Veuillez contacter votre représentant de compte Magnite pour plus d’informations.


Sur l’écran « Configurer un nom de fichier et un planning d’exportation pour chaque audience », vous devez maintenant configurer une date de début (obligatoire), une date de fin (facultatif) et un identifiant de mappage (obligatoire) pour chaque audience.

>[!IMPORTANT]
>
> Un ID de mappage ou « AUCUN » est requis pour cette destination.
>
> Un identifiant de mappage doit être fourni lorsqu’une audience possède un identifiant de segment préexistant connu précédemment pour la diffusion en continu Magnite. Sinon, « NONE » doit être utilisé comme ID de mappage.
>
> Lors de la configuration du nom de fichier pour chaque audience, incluez l’identifiant de mappage via le champ « Texte personnalisé » à ajouter. L’ID de mappage sera ajouté comme suit : `{previous_filename}\_\[MAPPING_ID\].` Si cette audience est nouvelle dans la diffusion en continu Magnite et que vous ne fournissez pas d’ID de mappage, « AUCUN » doit être saisi dans le champ « Texte personnalisé ». Dans ce cas, le nouveau nom de fichier doit être `{previous_filename}\_\[NONE\]`.

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois vos audiences chargées, vous pouvez vérifier qu’elles ont été créées et chargées correctement.

* La destination Magnite : Batch diffuse des fichiers S3 en flux continu Magnite à une cadence quotidienne. Après la diffusion et l’ingestion, les audiences/segments doivent apparaître dans la diffusion en continu Magnite et peuvent être appliqués à une offre. Vous pouvez le confirmer en recherchant l’identifiant du segment ou le nom du segment qui a été partagé lors des étapes d’activation dans le Adobe Experience Platform.

>[!NOTE]
>
>Audiences activées/diffusées vers Magnite : la destination par lots *remplacera* les mêmes audiences qui ont été activées/diffusées via la destination en temps réel Magnite. Si vous recherchez un segment à l’aide du nom de segment, vous pouvez ne pas trouver le segment en temps réel, jusqu’à ce que le lot ait été ingéré et traité par la plateforme de streaming Magnite.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour obtenir de la documentation d’aide supplémentaire, consultez le [Magnite Help Center](https://help.magnite.com/help).
