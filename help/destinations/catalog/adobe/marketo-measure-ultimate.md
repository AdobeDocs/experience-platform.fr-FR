---
title: Destination Marketo Measure Ultimate
description: Découvrez comment connecter et activer des données vers la destination Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 26%

---

# Destination Marketo Measure Ultimate {#mmu-destination}

## Vue d’ensemble {#overview}

Marketo Measure (anciennement Bizible) fournit aux marketeurs insight les actions marketing les plus efficaces pour générer du chiffre d’affaires et optimiser le retour sur investissement de leur entreprise. Marketo Measure est une solution d’attribution marketing qui effectue automatiquement le suivi et crée des rapports sur les performances des canaux, en offrant une visibilité sur les canaux qui génèrent le plus d’engagement des clients et en vous permettant d’optimiser vos dépenses marketing en conséquence.

La destination permet les flux de données B2B (business-to-business) de Adobe Experience Platform vers Marketo Measure. La carte n’est disponible que pour les clients Marketo Measure Ultimate .

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination Marketo Measure, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre. Cette intégration :

* Satisfait aux exigences complexes de données et de rapports sur les performances des grandes entreprises.
* Active le compte rendu des performances d’attribution B2B avec plusieurs systèmes de gestion de la relation client et d’automatisation marketing.
* Facilite l’importation de données de point de contact hors ligne tierces.

## Conditions préalables {#prerequisites}

Notez les conditions préalables suivantes pour la destination Marketo Measure :

* Le mappage du sandbox Experience Platform doit être effectué dans la page des paramètres de Marketo Measure par l’administrateur. Sans le mappage Sandbox, vous ne pouvez pas terminer le workflow pour vous connecter à l’enregistrement et à l’activation des données de destination.
* Seuls les jeux de données des classes XDM B2B peuvent être exportés (voir, par exemple, les classes XDM Business Account et XDM Business Opportunity). Vous ne pouvez pas importer plusieurs jeux de données de la même classe XDM B2B pour une source de données donnée.
* Chaque jeu de données ne peut être inclus que dans un flux de données vers la destination Marketo Measure.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Non | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Oui | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Dataset export]** | Vous exportez des jeux de données bruts, qui ne sont pas regroupés ou structurés par intérêt ou qualification d’audience. En savoir plus sur les [exportations de jeux de données](/help/destinations/destination-types.md#dataset-export-destinations). |
| Fréquence des exportations | **[!UICONTROL Batch]** | Cette destination par lots exporte des fichiers vers la plateforme Marketo Measure toutes les deux heures. En savoir plus sur la [planification d’exportations de jeux de données](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage and Activate Dataset Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration de la destination, renseignez les champs répertoriés dans la section ci-dessous.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

![Le workflow Se connecter à la destination pour la destination Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Exporter des jeux de données vers cette destination {#export-datasets}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage and Activate Dataset Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Lisez le tutoriel [Exporter des jeux de données](/help/destinations/ui/export-datasets.md) pour obtenir des instructions détaillées sur l’exportation de jeux de données vers cette destination.

## Valider l’exportation des données {#exported-data}

Pour valider une exportation réussie de jeu de données, vous pouvez vérifier que votre jeu de données a réussi à atteindre votre entrepôt de données [Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
