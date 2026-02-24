---
title: Connexion à la destination en temps réel Magnite
description: Utilisez cette destination pour diffuser des audiences Adobe CDP vers la plateforme de streaming Magnite en temps réel.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 4e08a14b-6800-41e1-95a5-826a6241144d
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 25%

---

# Magnite : connexion à la destination en temps réel

## Vue d’ensemble {#overview}

Les destinations [!DNL Magnite: Real-Time] et [Magnite : lot](/help/destinations/catalog/advertising/magnite-batch.md) de Adobe Experience Platform vous permettent de mapper et d’exporter des audiences pour le ciblage et l’activation sur la plateforme de streaming Magnite.

L’activation des audiences sur la plateforme [!DNL Magnite Streaming] est un processus en deux étapes qui nécessite l’utilisation des destinations Magnite : Real-Time et Magnite : Batch .

Pour activer vos audiences dans [!DNL Magnite Streaming], vous devez :

* Activez les audiences sur la destination [!DNL Magnite: Real-Time], comme illustré sur cette page.
* Activez la même audience sur la destination Magnite : lot . La destination [!DNL Magnite: Batch] est un composant obligatoire. Si vous n’activez pas l’audience sur la destination par lots [!DNL Magnite Streaming] , l’intégration échouera et vos audiences ne seront pas activées.

Remarque : lors de l’utilisation de la destination en temps réel, [!DNL Magnite Streaming] recevrez des audiences en temps réel, mais Magnite ne peut stocker que temporairement des audiences en temps réel dans sa plateforme et elles seront supprimées du système dans un délai de deux jours. Pour cette raison, si vous souhaitez utiliser la destination Magnite : Real-Time , vous devez *également* utiliser la destination Magnite : Batch . Pour chaque audience que vous activez vers la destination Real-Time , vous devez également activer vers la destination Batch .

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Magnite]. Pour toute demande ou information, contactez directement l’équipe d’Amazon Ads au `adobe-tech@magnite.com`.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Magnite: Real-Time], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Activation et ciblage {#activation-and-targeting}

Cette intégration à Magnite permet aux clients de transmettre leurs audiences CDP de Adobe Experience Platform à Magnite pour le ciblage publicitaire. Les audiences peuvent être sélectionnées dans Magnite pour le ciblage positif et le ciblage négatif (suppression).

## Conditions préalables {#prerequisites}

Pour utiliser les destinations [!DNL Magnite] dans Adobe Experience Platform, vous devez d’abord disposer d’un compte [!DNL Magnite Streaming]. Si vous disposez d’un compte [!DNL Magnite Streaming], contactez votre gestionnaire de compte [!DNL Magnite] afin d’obtenir des informations d’identification pour accéder aux destinations [!DNL Magnite's].
Si vous n’avez pas de compte [!DNL Magnite Streaming], veuillez contacter adobe-tech@magnite.com

## Identités prises en charge {#supported-identities}

La destination [!DNL Magnite: Real-Time] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Un identifiant unique pour un appareil ou une identité. Nous acceptons n’importe quel identifiant d’appareil et identifiant propriétaire, quel que soit son type. | Les types d’identité pris en charge par Magnite incluent, sans s’y limiter, les identifiants PPUID, GAID, IDFA et d’appareil de télévision. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

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

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type d’exportation | **[!UICONTROL Segment export]** | Vous exportez tous les membres d’un segment (audience) ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Magnite: Real-Time]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View destinations]** et **[!UICONTROL Manage destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

![champs d’authentification de la configuration de destination vides](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Username]** : nom d’utilisateur qui vous a été fourni par [!DNL Magnite].
* **[!UICONTROL Password]** : mot de passe qui vous a été fourni par [!DNL Magnite].

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Your company name]** : nom de votre client/société. Seuls les clients [!DNL Magnite Streaming] pris en charge peuvent être sélectionnés.

>[!NOTE]
>
>Le nom de la société doit être une chaîne correspondant au nom du compartiment de diffusion Amazon S3 que vous avez configuré avec Magnite et configuré à l’étape [s’authentifier à la destination](#authenticate). Les caractères pris en charge sont « a-z », « A-Z », « 0-9 », « - » (tiret) ou « _ » (trait de soulignement).

![champs d’authentification de la configuration de destination renseignés](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Une fois que vous avez terminé, cliquez sur le bouton **[!UICONTROL Create]** .

![Politique de gouvernance facultative et mesures d’application](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View destinations]**, **[!UICONTROL Activate destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Une fois la connexion de destination créée, vous pouvez passer au flux d’activation de l’audience. La section suivante explique comment activer des audiences à l’aide de la destination en temps réel.

### Mapper les attributs et les identités {#map}

L’étape suivante consiste à mapper les identifiants source à l’identifiant Device_id Magnite.

* Vous pouvez ajouter autant de mappages que nécessaire en sélectionnant **[!UICONTROL Add new mapping]**.

Cet exemple utilisant la destination en temps réel affiche une ligne contenant un identifiant source deviceId générique mappé au champ cible Device_id Magnite. Lorsque vous utilisez les mappages, sélectionnez [!UICONTROL Next].

![Mappez les champs de données de votre choix au champ device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Veillez à définir les ID de mappage sur toutes les audiences activées ou à définir la valeur AUCUN en l’absence d’ID de mappage.

![Veillez à définir les ID de mappage sur toutes les audiences activées ou à définir la valeur AUCUN en l’absence d’ID de mappage](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Vous devez maintenant configurer une date de début (obligatoire), une date de fin (facultatif) et un identifiant de mappage pour chaque audience.

**Identifiant de mappage**

* Utilisez le champ **[!UICONTROL Mapping ID]** lorsqu’une audience possède un identifiant de segment préexistant connu précédemment de Magnite.

* Pour ajouter un **[!UICONTROL Mapping ID]** à une audience, sélectionnez chaque ligne d’audience individuellement et saisissez les données dans la colonne de droite (voir l’image ci-dessus). Si vous ne souhaitez pas ajouter d’ID de mappage, saisissez AUCUN dans le champ ID de mappage .

Sélectionnez **[!UICONTROL Next]** et finalisez le flux d’activation.

![Sélectionnez suivant et finalisez le flux d’activation.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois vos audiences chargées, vous pouvez vérifier qu’elles ont été créées et chargées correctement en procédant comme suit :

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Après l’ingestion, les audiences doivent apparaître dans [!DNL Magnite Streaming] dans les minutes qui suivent et peuvent être appliquées à une transaction. Vous pouvez le confirmer en recherchant l’identifiant du segment qui a été partagé lors des étapes d’activation dans le Adobe Experience Platform.

## Activer les mêmes audiences via la [!DNL Magnite: Batch]destination

Les audiences partagées avec [!DNL Magnite Streaming] à l’aide de la destination en temps réel devront également être partagées à l’aide de la destination Magnite : Batch . Lorsque la configuration est correcte, les noms de segment dans l’interface utilisateur de [!DNL Magnite Streaming] sont mis à jour pour refléter ceux utilisés dans la mise à jour post-quotidienne de Adobe Experience Platform.

Enfin, si une destination par lots n’a pas été configurée pour votre intégration, configurez-la maintenant via le document Magnite : Destination par lots .

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour obtenir de la documentation d’aide supplémentaire, consultez le [Magnite Help Center](https://help.magnite.com/help).
