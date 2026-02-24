---
title: Audiences Experience Cloud
description: Découvrez comment partager des audiences de Real-Time Customer Data Platform vers différentes applications Experience Cloud.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 13%

---


# Connexion [!UICONTROL Experience Cloud Audiences]

>[!AVAILABILITY]
>
> Cette destination est disponible pour les clients [Adobe Real-Time Customer Data Platform Prime et Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

Utilisez cette destination pour activer des audiences de Real-Time CDP vers Audience Manager et Adobe Analytics.

Pour envoyer des audiences à Adobe Analytics, vous avez besoin d’une licence Audience Manager. Pour plus d’informations, consultez la présentation d’[Audience Analytics](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=fr).

Pour envoyer des audiences à d’autres solutions Adobe, utilisez les connexions directes de Real-Time CDP vers [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) et [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Cette destination remplace l’[ancienne intégration du partage d’audiences](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-in-aam) de Real-Time Customer Data Platform vers différentes solutions Experience Cloud.
> 
>Si vous partagez déjà des audiences de Real-Time CDP vers Audience Manager et d’autres solutions Experience Cloud par le biais de l’[ancienne intégration de partage d’audiences](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-in-aam), vous devez contacter l’assistance clientèle pour désactiver l’ancienne intégration avant d’utiliser cette destination.

![Destination des audiences Experience Cloud, mise en surbrillance dans le catalogue des destinations.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Cas d’utilisation et avantages {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!UICONTROL Experience Cloud Audiences], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Real-Time CDP peut résoudre.

### Activation des cas d’utilisation de Data Management Platform {#dmp-use-cases}

Dans Audience Manager, vous pouvez utiliser les audiences Real-Time CDP pour les cas d’utilisation de Data Management Platform, tels que :

* Ajouter des [données tierces](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=fr#third-party-data) à vos segments ;
* [modélisation algorithmique](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=fr);
* L’activation de vos audiences vers des destinations basées sur des cookies qui ne sont pas encore prises en charge dans le catalogue des destinations Real-Time CDP.

### Contrôle granulaire des audiences exportées {#segments-control}

Pour sélectionner les audiences à exporter vers Audience Manager et au-delà, utilisez la nouvelle intégration de partage d’audiences en libre-service via la destination Audiences d’Experience Cloud .  Cela vous permet de déterminer les audiences que vous souhaitez partager avec d’autres solutions Experience Cloud et celles que vous souhaitez conserver exclusivement dans Real-Time CDP.

L’ancienne intégration de partage d’audiences ne permettait pas un contrôle granulaire des audiences à exporter vers Audience Manager et au-delà.

### Partager des audiences Real-Time CDP avec Adobe Analytics {#share-audiences-with-analytics}

Les audiences que vous envoyez à la destination Audiences Experience Cloud n’apparaissent pas automatiquement dans Adobe Analytics.

Avant d’envoyer des audiences à Adobe Analytics, vous devez [mettre en œuvre le service Experience Cloud Identity pour Analytics et Audience Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=fr).

>[!IMPORTANT]
>
>Pour envoyer des audiences de Real-Time CDP vers Adobe Analytics via la destination Audiences d’Experience Cloud, vous devez disposer d’une licence Audience Manager.

### Partage d’audiences Real-Time CDP avec d’autres solutions Experience Cloud {#share-segments-with-other-solutions}

Vous pouvez utiliser la carte de destination Audiences Real-Time CDP pour partager des audiences avec d’autres solutions Experience Cloud.

Cependant, Adobe recommande vivement d’utiliser les cartes de destination dédiées suivantes si vous souhaitez partager des audiences avec ces solutions :

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
> * Vous avez besoin d’une licence Audience Manager pour activer les [cas d’utilisation de la plateforme de gestion des données](#dmp-use-cases) mentionnés plus haut.
> * Vous *avez* besoin d’une licence Audience Manager pour partager des audiences Real-Time CDP avec Adobe Analytics.
> * Vous *pas besoin* d’une licence Audience Manager pour partager des audiences Real-Time CDP avec Adobe Advertising Cloud, Adobe Target, Marketo et d’autres solutions Experience Cloud, mentionnées dans la [section ci-dessus](#share-segments-with-other-solutions).

### Pour les clients qui utilisent la solution de partage d’audience héritée

Si vous partagez déjà des audiences de Real-Time CDP vers Audience Manager et d’autres solutions Experience Cloud par le biais de l’[ancienne intégration de partage d’audiences](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-in-aam), vous devez contacter l’assistance clientèle pour désactiver l’ancienne intégration.

Le délai de résolution du ticket de déprovisionnement est de six jours ouvrables ou moins. Une fois l’intégration héritée existante désactivée, vous pouvez passer à [créer une connexion](#connect) via la carte de destination en libre-service.

>[!IMPORTANT]
>
>L’exportation de l’audience de Real-Time CDP vers vos autres solutions est arrêtée entre la résolution du ticket et le moment où une nouvelle connexion est établie via la carte de destination. Vous pouvez minimiser ce temps d’arrêt en créant la connexion via la carte de destination une fois le ticket fermé.

## Limites et légendes connues {#known-limitations}

Notez les limites connues et les légendes importantes suivantes lors de l’utilisation de la carte Audiences Experience Cloud :

* Actuellement, vous pouvez configurer la destination Audiences d’Experience Cloud sur un seul sandbox par organisation. Toute tentative de configuration d’une seconde connexion de destination dans un autre sandbox entraîne une erreur.
* Lors de la connexion à la destination, une option permettant d’[activer les alertes de flux de données](../../ui/alerts.md) s’affiche. Bien que visible dans l’interface utilisateur, l’option **Activer les alertes n’est actuellement pas prise en charge**.
* **Prise en charge du renvoi de l’audience** : la première exportation vers Audience Manager ou d’autres solutions Experience Cloud comprend une population historique des audiences. Les utilisateurs de l’[ancienne intégration de partage d’audience](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-in-aam) qui configurent cette destination doivent s’attendre à une différence de renvoi d’environ six heures.
* Les audiences issues de [Composition de l’audience](../../../segmentation/ui/audience-composition.md) ne sont pas directement prises en charge. Pour activer les audiences composites vers cette destination, vous devez créer une définition d’audience via [Créateur de segments](../../../segmentation/ui/segment-builder.md) basée sur votre audience composite, et activer l’audience nouvellement créée.

### Latence lors de l’activation des audiences {#audience-activation-latency}

Il existe une latence de quatre heures entre le moment où les audiences sont activées pour la première fois dans Real-Time CDP et le moment où elles sont prêtes à être utilisées dans Audience Manager et d’autres solutions Experience Cloud.

La disponibilité complète des audiences dans Audience Manager pour tous les cas d’utilisation peut prendre jusqu’à 24 heures. L’affichage des audiences d’Experience Cloud Audiences dans les rapports Audience Manager peut prendre jusqu’à 48 heures.

Les métadonnées, telles que les noms d’audience, sont disponibles dans Audience Manager dans les minutes qui suivent la configuration de l’exportation vers la destination Audiences Experience Cloud.

## Identités prises en charge {#supported-identities}

Les profils exportés vers la destination [!UICONTROL Experience Cloud Audiences] sont mappés aux identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| ECID | Experience Cloud ID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Pour plus d’informations, consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) . |
| GAID | GOOGLE ADVERTISING ID | Les profils ingérés dans Real-Time CDP avec une identité principale Google Advertising ID (GAID) peuvent être exportés vers cette destination. |
| IDFA | Identifiant Apple pour les annonceurs | Les profils ingérés dans Real-Time CDP avec une identité principale Apple ID for Advertisers (IDFA) peuvent être exportés vers cette destination. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Les profils ingérés dans Real-Time CDP avec une identité principale d’adresse e-mail hachée peuvent être exportés vers cette destination. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audience que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

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
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience dont les identités sont désactivées dans la section ci-dessus. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Real-Time CDP en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Set up]** dans la vue Carte de destination du catalogue et sélectionnez **[!UICONTROL Connect to destination]**.

![Vue de l’option Se connecter à la destination pour la destination Audiences Experience Cloud.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Configurer un nouvel écran de destination affichant les paramètres obligatoires et facultatifs pour la connexion à la destination Audiences Experience Cloud.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Lisez [Activer des profils et des audiences vers des destinations d’exportation d’audiences de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination. Aucune [&#x200B; étape de mappage &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) n’est requise et aucune [&#x200B; étape de planification &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) n’est disponible pour cette destination.

## Valider l’exportation des données {#exported-data}

Pour valider l’exportation réussie des données, vous pouvez vérifier que vos audiences ont réussi à atteindre la solution Experience Cloud souhaitée.

### Validation des données dans Audience Manager

Vos audiences Real-Time CDP apparaissent dans Audience Manager sous la forme de [signaux](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-as-aam-signals), [caractéristiques](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-as-aam-traits) et [segments](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr#aep-segments-as-aam-segments). Vous pouvez vérifier dans Audience Manager si les données se sont affichées comme décrit dans les liens vers la documentation ci-dessus.

Les noms de segment commencent à être renseignés dans Audience Manager 15 minutes après l’envoi des audiences depuis Real-Time CDP.

La population de segments commence à affluer dans Audience Manager dans les 6 heures suivant son envoi à partir de Real-Time CDP et est mise à jour toutes les 24 heures dans Audience Manager.

La population complète sera visible dans Audience Manager au bout de 72 heures et les populations continueront à circuler vers Audience Manager à moins que l’audience ne soit supprimée de la destination dans Real-Time CDP.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Real-Time CDP] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

La gouvernance des données dans Real-Time CDP est appliquée à la fois par des [libellés d’utilisation des données](/help/data-governance/labels/reference.md) et des actions marketing.
Les libellés d’utilisation des données sont transférés vers les applications, contrairement aux actions marketing. Cela signifie qu’une fois qu’elles arrivent dans Audience Manager, les audiences de Real-Time CDP peuvent être exportées vers n’importe quelle destination disponible. Dans Audience Manager, vous pouvez utiliser des [contrôles d’exportation des données](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=fr) pour bloquer l’exportation d’audiences vers certaines destinations.

Les audiences marquées avec l’action marketing [!DNL HIPAA] ne sont pas envoyées de Real-Time CDP vers Audience Manager.

### Gestion des autorisations dans Audience Manager

Les audiences et les caractéristiques dans Audience Manager sont soumises au [contrôle d’accès en fonction du rôle](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=fr) (RBAC).

Les audiences exportées depuis Real-Time CDP sont affectées à une source de données spécifique dans Audience Manager appelée **[!UICONTROL Experience Platform Segments]**.

Pour autoriser uniquement certains utilisateurs à accéder aux audiences, utilisez [Contrôles d’accès en fonction du rôle](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=fr) pour configurer l’accès des utilisateurs et utilisatrices aux audiences et caractéristiques créées à partir des audiences Real-Time CDP.
