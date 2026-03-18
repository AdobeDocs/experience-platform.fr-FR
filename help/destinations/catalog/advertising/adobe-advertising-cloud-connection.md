---
title: Connexion Adobe Advertising DSP
description: Découvrez comment partager des audiences propriétaires authentifiées et non authentifiées avec Adobe Advertising Cloud Demand-Side Platform (DSP) à l’aide de plusieurs types d’identité.
feature: Destinations
source-git-commit: 5513e95637c1016caeb6abe699e1807cc234ed40
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 16%

---


# Connexion Adobe Advertising DSP

## Vue d’ensemble {#overview}

La destination Adobe Advertising Cloud Demand-Side Platform (DSP) permet aux utilisateurs de partager des audiences propriétaires authentifiées et non authentifiées avec un compte DSP ou un annonceur spécifique au sein d’un compte.

Cette destination permet aux clients de partager des audiences propriétaires avec l’un de ces identifiants ou tous :

* Identifiant d’e-mail haché, converti en [!DNL LiveRamp RampID] ou [!DNL Unified ID 2.0] (UID2.0) pour le ciblage dans DSP

* Cookies tiers Experience Cloud ID (ECID) et Adobe Advertising

* Identifiants publicitaires mobiles (MAID) :

   * [!DNL Google] des identifiants Advertising (GAID) pour les appareils [!DNL Android]

   * Identifiants pour les annonceurs (IDFA) pour les appareils [!DNL Apple iOS]

Cette connexion remplace l’ancienne [connexion Adobe Advertising Cloud DSP](adobe-advertising-cloud-connection-legacy.md), qui ne prend en charge que les adresses e-mail hachées.

>[!IMPORTANT]
>
>Cette page a été créée par l’équipe Adobe Advertising [!DNL DSP]. Pour toute demande ou information, contactez directement l’assistance Advertising Cloud à l’adresse `adcloud_support@adobe.com`.

## Cas d’utilisation {#use-cases}

Cette destination permet aux annonceurs d’atteindre leur audience sur plusieurs navigateurs avec et sans cookies.

Les annonceurs ont le choix de partager des segments avec des identifiants propriétaires authentifiés (tels que [!DNL RampID] et [!DNL UID2.0]) ou sous la forme d’identifiants non authentifiés (tels que des cookies et des MAID).

## Conditions préalables {#prerequisites}

* Par [!DNL RampID activation], [!DNL DSP] les paramètres au niveau du compte et de la campagne pour activer le partage d’audience avec [!DNL LiveRamp RampID], qui convertit les données client en [!DNL RampIDs] pour créer des segments cibles. Votre équipe de compte Adobe effectuera cette configuration. [!DNL RampID] est disponible via un partenariat entre [!DNL DSP] et [!DNL LiveRamp], et vous n&#39;avez pas besoin de votre propre adhésion [!DNL LiveRamp] pour l&#39;utiliser.

* ID d’audience :

   * Pour [!DNL RampID] et [!DNL UID2.0], les profils doivent contenir des identifiants d’e-mail hachés.

   * Pour les cookies, configurez un processus de synchronisation des cookies avec [!DNL Web SDK] flux de données ou l’[!DNL Experience Cloud ID Service] . Voir [Configurer la synchronisation des identifiants pour partager des cookies](#cookie-sync) ci-dessous.

   * Pour les profils avec MAID :

      * Pour chaque GAID, incluez la valeur `GAID` dans une colonne IdentityMap .

      * Pour chaque IDFA, incluez la valeur `IDFA` dans une colonne IdentityMap .

* Identifiant d’organisation Experience Cloud du compte Experience Platform. Votre identifiant figure sur la page de votre profil utilisateur Adobe Real-Time Customer Data Platform (Real-Time CDP).

* Une source [Real-Time CDP dans DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) pour recevoir les audiences pour l’activation de la campagne. L’équipe de votre compte Adobe crée la source à l’aide de votre ID d’organisation Experience Cloud.

* Clé source du compte [!DNL DSP] ou de l’annonceur, générée lors de la création d’une source Real-Time CDP [dans [!DNL DSP]](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). L’équipe de votre compte [!DNL DSP] partagera cette clé avec vous. Vous l’utiliserez dans Experience Platform pour créer une connexion de destination à la destination Advertising Cloud DSP, comme expliqué ci-dessous.

### Configurer la synchronisation des identifiants pour partager des cookies {#cookie-sync}

La synchronisation des identifiants est une condition préalable au partage de cookies tiers. Configurez un processus de synchronisation des cookies avec [!DNL Web SDK] flux de données ou le [!DNL Experience Cloud ID Service] . Pour plus d’informations sur la gestion des identités pour les cookies tiers, consultez [Destinations Advertising reposant sur des intégrations de cookies tiers](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Activer la synchronisation des identifiants tiers avec[!DNL Web SDK]**

Si vous utilisez [!DNL Experience Platform Web SDK], activez la synchronisation des identifiants tiers sur votre flux de données en configurant l’option [!UICONTROL Third Party ID Sync] dans les paramètres avancés. Pour obtenir des instructions, voir [Configurer les options avancées](/help/datastreams/configure.md#advanced-options) dans la documentation sur les flux de données.

**Activer la synchronisation des identifiants tiers avec le[!DNL Experience Cloud ID Service]**

Si vous utilisez des balises [!DNL Experience Platform] avec le [!DNL Experience Cloud ID Service], configurez la synchronisation des identifiants tiers à l’aide de l’extension du service Experience Cloud ID [](/help/tags/extensions/client/id-service/overview.md). Cela permet au cookie Adobe Advertising correspondant à l’ECID donné d’être disponible lorsque vous activez l’audience à partir de Real-Time CDP.

## Identités prises en charge {#supported-identities}

La destination Adobe Advertising Cloud DSP prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | Adresses e-mail hachées avec l’algorithme SHA256 | Experience Platform prend en charge le texte brut et les adresses e-mail hachées SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour qu’Experience Platform hache automatiquement les données lors de l’activation. |
| `ECID` | Cookie propriétaire pour Experience Cloud | Obligatoire pour créer des segments basés sur des cookies. |
| `Everesttech cookie` | Cookie tiers pour Adobe Advertising | Obligatoire pour créer des segments basés sur des cookies. |
| `GAID` | ID d’appareil [!DNL Android] | Requis pour le ciblage des appareils [!DNL Android]. |
| `IDFA` | ID d’appareil [!DNL iOS] | Requis pour le ciblage des appareils [!DNL iOS]. |

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
| -------------------- | --------- | ----------- | --------- |
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau suivant pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
| ---- | ---- | ----- |
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants sélectionnés. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions) d’Experience Platform. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à la destination, suivez les instructions [création d’une connexion de destination](/help/destinations/ui/connect-destination.md) à l’aide de l’interface utilisateur d’Experience Platform. Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les sous-sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous connecter à la destination, indiquez le paramètre suivant dans la section [!UICONTROL Connection type], puis sélectionnez **[!UICONTROL Connect to destination]** :

* **[!UICONTROL Account or Advertiser Key]** : ce [!UICONTROL Source Key] est généré lorsqu’une source [Real-Time CDP est créée dans l’interface utilisateur de DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). L’équipe de votre compte Adobe partagera cette clé avec vous après la création de la source.

![Copie d’écran de la section Type de connexion affichant le champ Compte ou clé de l’annonceur.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

![Copie d’écran des champs de détails de destination affichant les entrées Nom et Description.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des identités, vous avez besoin de l’autorisation **[!UICONTROL View Identity Graph]** [contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Vous pouvez choisir les identifiants à envoyer à Adobe Advertising DSP. Par défaut, les identifiants de cookie sont sélectionnés pour l’annonceur. Vous pouvez également choisir d’ajouter des [!UICONTROL Hashed Email], des [!UICONTROL IDFA] et des [!UICONTROL GAID].

Pour obtenir des instructions, voir [Mappage des attributs et des identités](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

![Capture d’écran de la section de mappage d’identité présentant les identifiants de cookie, les e-mails hachés, les options IDFA et GAID.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

## Valider l’exportation des données {#exported-data}

Pour vérifier que les données d’audience ont été partagées avec Advertising Cloud, vérifiez les éléments suivants :

* Le flux de données dans la destination [!DNL Real-Time CDP] a réussi.

* Dans DSP, l’audience est disponible lorsque vous créez ou modifiez une audience à partir de **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** ou dans la section **[!UICONTROL Audience Targeting]** des paramètres d’emplacement. L’audience doit être visible dans l’onglet [!UICONTROL Adobe Segments] sous le dossier [!UICONTROL Real-Time CDP] .

![audiences Real-Time CDP dans les paramètres d’audience DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](/help/data-governance/home.md).
