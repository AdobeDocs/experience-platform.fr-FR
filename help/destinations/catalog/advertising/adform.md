---
title: Adform
description: Adform est un fournisseur de premier plan de solutions d'achat et de vente de médias programmatiques. En connectant Adform au Adobe Experience Platform, vous pouvez activer vos audiences propriétaires via Adform en fonction de l’Experience Cloud ID (ECID).
last-substantial-update: 2025-10-23T00:00:00Z
source-git-commit: c429ee227bd93455f541a32266bfbef9ddeaae06
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 32%

---


# Connexion à Adform {#adform}

## Vue d’ensemble {#overview}

Adform est un fournisseur de premier plan de solutions d&#39;achat et de vente de médias programmatiques. En connectant Adform au Adobe Experience Platform, vous pouvez activer vos audiences propriétaires via Adform en fonction de l’Experience Cloud ID (ECID).

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe d’Adobe. Pour toute demande ou information, contactez directement l’équipe d’Amazon Ads au `support@adform.com`.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination Adform, consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Activation d’une audience Adobe Real-Time CDP {#use-case-1}

Utilisez cette destination pour envoyer des audiences Adobe Real-Time CDP à Adform pour activation en fonction de l’Experience Cloud ID (ECID) et de l’ID Fusion d’Adform. ID Fusion d’Adform est le service de résolution d’ID d’Adform qui vous permet d’activer vos audiences propriétaires en fonction de l’Experience Cloud ID (ECID).

Un cas courant est le reciblage des visiteurs de votre site web ou de votre application en fonction de l’Experience Cloud ID (ECID). Il vous suffit d’envoyer l’Experience Cloud ID (ECID) à Adform via les extensions Adform [Event Streaming](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) ou [côté client](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/catalog/analytics/adform) facilement disponibles. Ensuite, vous pouvez partager des audiences avec Adform via la destination Adform pour l’activation, uniquement en fonction de l’Experience Cloud ID (ECID).

## Conditions préalables {#prerequisites}

* Vous devez être un client ou une cliente Adobe existant(e) pour utiliser cette destination.
* Vous devez disposer des informations d’identification de connexion aux données d’Adobe Audience Base.
   * Si vous ne disposez pas des informations d’identification de connexion aux données d’Adform Audience Base, contactez votre représentant ou représentante Adform.
* Pour une synchronisation correcte, vous devez disposer d’une connexion [diffusion en continu d’événements](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) ou [côté client](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/catalog/analytics/adform) de vos entités à Adform Site Tracking.
   * Si vous ne disposez pas d’une connexion en continu d’événements ou côté client de vos entités au suivi de site Adform, contactez votre représentant Adform.
   * Adform fournit des extensions Adobe Experience Cloud pour [diffusion en continu d’événements](https://exchange.adobe.com/apps/ec/600102/adform-s2s-site-tracking) et [côté client](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/catalog/analytics/adform).


## Identités prises en charge {#supported-identities}

Adform prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| ECID | Experience Cloud ID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Pour plus d’informations, consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) . |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Segment export]** | Vous exportez tous les membres d’un segment (audience) ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *YourDestination*. |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

![S’authentifier auprès de la destination](../../assets/catalog/advertising/adform/authenticate-destination.png)

* **[!UICONTROL Account name]** : saisissez un nom de compte par lequel vous pourrez identifier cette connexion de destination à l’avenir..
* **[!UICONTROL S3 Access Key ID]** : renseignez la clé d’accès S3 fournie par Adform.
* **[!UICONTROL S3 Secret Access Key]** : renseignez la clé d’accès secrète S3 fournie par Adform.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Renseigner les détails de la destination](../../assets/catalog/advertising/adform/configure-destination-details.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Provider Name]** : nom de compte fourni par Adform.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

* **ECID** (Experience Cloud ID)

Pendant l’étape de mappage, utilisez uniquement le mappage d’identité cible [!DNL ECID]. N’incluez aucun autre champ d’identité, car cela empêchera l’activation de se terminer correctement.

## Données exportées / Valider l’exportation des données {#exported-data}

Le connecteur de destination exporte uniquement l’identité ECID vers la destination. Aucune autre identité n’est exportée. Pour vérifier si l’exportation des données a réussi, connectez-vous à votre compte Adobe Audience Base et vérifiez si les audiences sont disponibles.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur Adform Audience Base, consultez la [documentation d’Adform Audience Base](https://www.adformhelp.com/hc/en-us/categories/9738365991697-Data-Management-Platform).