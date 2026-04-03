---
title: Surveiller la segmentation Edge
description: Découvrez comment utiliser le tableau de bord de surveillance pour observer le débit de segmentation Edge.
exl-id: 7abba7e8-1f2d-4a21-a93f-8bda7aa4d849
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 6%

---

# Surveiller la segmentation Edge

Vous pouvez utiliser le tableau de bord de surveillance dans l’interface utilisateur de Adobe Experience Platform pour effectuer une surveillance en temps réel de la segmentation Edge au sein de votre organisation. Utilisez cette fonctionnalité pour accéder à une plus grande transparence dans le débit de vos données Edge.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Flux de données](../../datastreams/overview.md) : les flux de données vous permettent de connecter Experience Platform Edge Network à votre jeu de données.
* [Capacités](../../landing/license-usage-and-guardrails/capacity.md) : dans Experience Platform, les capacités vous permettent de savoir si votre organisation a dépassé l’un de vos mécanismes de sécurisation et vous donnent des informations sur la manière de résoudre ces problèmes.
* [segmentation Edge ](../../segmentation/methods/edge-segmentation.md) : la segmentation Edge permet d’évaluer instantanément les définitions de segment dans Adobe Experience Platform [sur le serveur Edge](../../landing/edge-and-hub-comparison.md), en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

## Accès {#access}

Pour accéder au tableau de bord de surveillance du débit de segmentation Edge, sélectionnez **[!UICONTROL Monitoring]** dans la section **[!UICONTROL Data management]** , puis **[!UICONTROL Edge]**.

![La méthode d’accès au tableau de bord de segmentation Edge de la surveillance est mise en surbrillance.](/help/dataflows/assets/ui/monitor-edge/access.png)

Le tableau de bord de surveillance s’affiche. Vous y trouverez des mesures de surveillance du débit de diffusion en continu Edge, un graphique affichant le taux de débit de diffusion en continu Edge et une vue de flux de données. Ces mesures peuvent être filtrées par service, par Edge et par date.

![Les options de filtrage du tableau de bord de surveillance sont mises en surbrillance.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>Vous pouvez afficher la vue Flux de données **uniquement** si vous sélectionnez [!UICONTROL Edge segmentation throughput].

Si vous filtrez par service, vous pouvez choisir le service à propos duquel vous souhaitez afficher les informations de débit. Cela inclut des services tels que la segmentation Edge, la collecte de données, Target, Adobe Journey Optimizer, Offer Decisioning, les destinations personnalisées, le transfert d’événement, Adobe Analytics et Adobe Audience Manager.

Si vous filtrez par arête, vous pouvez choisir l’arête sur laquelle vous souhaitez afficher des informations. Les périphéries prises en charge comprennent la côte Est des États-Unis, la côte Ouest des États-Unis, l’Europe, l’Inde, Singapour, l’Australie, le Japon et la Suisse. Vous pouvez sélectionner plusieurs arêtes à afficher à la fois.

Si vous filtrez par date, vous pouvez choisir l’échelle de temps pour filtrer vos événements. Cette échelle de temps peut être configurée sur 30 jours. Vous pouvez également utiliser l’une des échelles de temps préconfigurées suivantes : [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] et [!UICONTROL Last 30 days].

## Surveillance des mesures de débit Edge

Le tableau des mesures fournit des informations spécifiques au débit Edge du service sélectionné. Reportez-vous au tableau suivant pour plus de détails sur chaque colonne.

| Mesure | Description |
| ------ | ----------- |
| Demandes reçues | Nombre de requêtes reçues par les périphéries sélectionnées au cours de la période. |
| Débit maximal | Taux de requêtes le plus élevé reçu par les périphéries sélectionnées au cours de la période. |

{style="table-layout:auto"}

## Graphique de surveillance du débit de segmentation Edge

Le graphique de surveillance affiche les enregistrements par seconde reçus par les périphéries sélectionnées au cours de la période allouée, par rapport à la capacité maximale autorisée.

![Le graphique de débit de segmentation Edge s’affiche.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## Vue du train de données

>[!NOTE]
>
>La vue du flux de données est **uniquement** disponible si vous filtrez le débit de segmentation d’Edge.

La section vue du flux de données affiche une liste des derniers flux de données ayant transité par les périphéries du sandbox.

![La vue du flux de données s’affiche, affichant des informations sur les flux de données répertoriés.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Champ | Description |
| ----- | ----------- |
| Nom du train de données | Nom du flux de données. |
| Jeux de données | Nom des jeux de données auxquels le flux de données appartient. |
| Service activé | Noms des services pour lesquels le flux de données est activé. |
| Demandes | Nombre de requêtes ayant transité par le flux de données. |
| Débit maximal | Taux le plus élevé de requêtes ayant transité par le flux de données. |
