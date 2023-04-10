---
title: (Version bêta) Audiences Experience Cloud
description: Découvrez comment partager des segments d’Experience Platform vers différentes solutions d’Experience Platform.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 24%

---


# (Version bêta) [!UICONTROL Audiences Experience Cloud] connection

Cette destination vous permet de partager des segments d’Experience Platform vers différentes solutions d’Experience Cloud, telles que Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo.

![La destination Audiences Experience Cloud, mise en surbrillance dans le catalogue des destinations.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Cette destination remplace la variable [intégration du partage de segment hérité](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) de l’Experience Platform à diverses solutions Experience Cloud.
>* Cette destination est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.


## Cas d’utilisation et avantages {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!UICONTROL Audiences Experience Cloud] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Activation des cas d’utilisation de Data Management Platform {#dmp-use-cases}

Dans Audience Manager, vous pouvez utiliser des segments Experience Platform pour les cas d’utilisation de Data Management Platform, tels que :

* Ajouter [données tierces](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) à vos segments ;
* [La modélisation algorithmique](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Activez vos segments vers des destinations basées sur des cookies qui ne sont pas encore prises en charge dans le catalogue des destinations Experience Platform.

### Contrôle granulaire des segments exportés {#segments-control}

Utilisez la nouvelle intégration du partage de segments en libre-service via la destination Audiences Experience Cloud pour sélectionner les segments à exporter vers l’Audience Manager et au-delà. Vous pouvez ainsi déterminer les segments que vous souhaitez partager avec d’autres solutions Experience Cloud et ceux que vous souhaitez conserver exclusivement en Experience Platform.

L’intégration de partage de segment héritée ne permettait pas de contrôler précisément quels segments devaient être exportés vers l’Audience Manager et au-delà.

### Partage de segments Experience Platform avec d’autres solutions Experience Cloud {#share-segments-with-other-solutions}

Outre le partage de segments avec l’Audience Manager, la carte de destination Audiences Experience Platform vous permet de partager des segments avec toute autre solution Experience Cloud pour laquelle vous avez été configuré, notamment :

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
> * Cette destination est disponible pour [Adobe Real-time Customer Data Platform Prime et Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) clients.
> * Vous avez besoin d’une licence d’Audience Manager pour activer la variable [Cas d’utilisation de Data Management Platform](#dmp-use-cases) mentionné plus haut.
> * You *ne doivent pas* une licence d’Audience Manager permettant de partager des segments Experience Platform avec Adobe Advertising Cloud, Adobe Target, Marketo et d’autres solutions Experience Cloud, comme indiqué dans la section [section supérieure](#share-segments-with-other-solutions).


### Pour les clients qui utilisent la solution de partage de segments héritée

Si vous partagez déjà des segments de l’Experience Platform vers l’Audience Manager et d’autres solutions d’Experience Cloud via la variable [intégration du partage de segment hérité](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), vous devez contacter l’assistance clientèle ou votre équipe de compte d’Adobe pour désactiver l’intégration héritée. L’assistance clientèle et les équipes du compte d’Adobe doivent déposer un ticket Jira (voir le ticket de modèle AAM-52354) pour désactiver l’intégration.

Le délai d’activation pour résoudre le ticket de désapprovisionnement pour les clients bêta est de six jours ouvrables ou moins. Une fois l’intégration héritée existante désactivée, vous pouvez procéder à la [création d&#39;une connexion](#connect) via la carte de destination en libre-service.

>[!IMPORTANT]
>
>L’exportation du segment de l’Experience Platform vers vos autres solutions sera arrêtée entre la résolution du ticket Jira et le moment où une nouvelle connexion est établie par le biais de la carte de destination. Vous pouvez minimiser ce temps d’arrêt en créant la connexion via la carte de destination dès que le ticket Jira est fermé.

## Limites et légendes connues {#known-limitations}

Notez les limites connues suivantes et les légendes importantes dans la version bêta de la carte Audiences Experience Cloud :

* [Surveillance des flux de données](/help/dataflows/ui/monitor-destinations.md) n’est pas prise en charge.
* Lorsque vous vous connectez à la destination, vous pouvez voir une option permettant d’accéder à [activation des alertes de flux de données](#enable-alerts). Bien qu’elle soit visible dans l’interface utilisateur, la variable **l’option activer les alertes n’est pas prise en charge** dans la version bêta.
* **Les renvois ne sont pas pris en charge**. Le premier export vers Audience Manager ou d’autres solutions Experience Cloud n’inclut pas une population historique des segments.
* Dans la version bêta, vous pouvez créer **une connexion de destination unique à la destination Audiences Experience Cloud ;**, sur tous les environnements de test appartenant à votre organisation Experience Platform.
* Il existe une **latence de quatre heures** entre le moment où ces données sont activées dans Experience Platform et celui où elles sont prêtes à être utilisées dans Audience Manager et d’autres solutions Experience Cloud.

## Identités prises en charge {#supported-identities}

Profils exportés vers le [!UICONTROL Audiences Experience Cloud] Les destinations sont mappées aux identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Consultez le document suivant sur [ECID](/help/identity-service/ecid.md) pour plus d’informations. |
| GAID | Google Advertising ID | Les profils ingérés dans Experience Platform avec une identité Principale de Google Advertising ID (GAID) peuvent être exportés vers cette destination. |
| IDFA | Identifiant Apple pour les annonceurs | Les profils ingérés dans Experience Platform avec une identité Principale d’Apple ID for Advertisers (IDFA) peuvent être exportés vers cette destination. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Les profils ingérés dans l’Experience Platform avec une Principale identité d’adresse électronique hachée peuvent être exportés vers cette destination. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) en dehors des identités répertoriées dans la section ci-dessus. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

>[!IMPORTANT]
> 
>Dans la version bêta, vous pouvez créer une connexion de destination unique à la destination Audiences Experience Cloud, sur tous les environnements de test appartenant à votre organisation Experience Platform.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, sélectionnez **[!UICONTROL Configuration]** en mode d’affichage Carte de destination dans le catalogue, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Vue de l’option Se connecter à la destination pour la destination Audiences Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Configurez un nouvel écran de destination affichant les paramètres requis et facultatifs pour vous connecter à la destination Audiences Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.


## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination. Notez que non [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) est requis et non [étape de planification](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) est disponible pour cette destination.

## Valider l’exportation des données {#exported-data}

Pour valider une exportation de données réussie, vous pouvez vérifier que vos segments ont réussi à atteindre la solution Experience Cloud souhaitée.

### Validation des données dans Audience Manager

Vos segments Experience Platform apparaissent dans Audience Manager en tant que [signals](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [traits](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), et [segments](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Vous pouvez vérifier en Audience Manager si les données sont apparues comme décrit dans les liens de documentation ci-dessus.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

La gouvernance des données en Experience Platform est appliquée par les deux [libellés d’utilisation des données](/help/data-governance/labels/reference.md) et les actions marketing.
Les libellés d’utilisation des données seront transférés vers les applications, mais les actions marketing ne le seront pas. Cela signifie qu’une fois qu’ils arrivent en Audience Manager, les segments d’Experience Platform peuvent être exportés vers n’importe quelle destination disponible. Dans Audience Manager, vous pouvez utiliser [contrôles des exportations de données](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) pour empêcher l’exportation de segments vers certaines destinations.

### Gestion des autorisations dans Audience Manager

Les segments et les caractéristiques de l’Audience Manager sont soumis aux [Contrôles d’accès en fonction du rôle](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=fr) (RBAC).

Les segments exportés depuis un Experience Platform sont affectés à une source de données spécifique dans l’Audience Manager appelée **[!UICONTROL Segments Experience Platform]**.

Pour autoriser uniquement certains utilisateurs à accéder aux segments, vous pouvez appliquer des contrôles d’accès aux segments appartenant à la source de données. Vous devez définir de nouvelles autorisations de contrôle d’accès dans Audience Manager pour ces segments et caractéristiques créés à partir de segments Experience Platform.