---
title: Présentation de l’hygiène de données
description: Le nettoyage de données d’Adobe Experience Platform vous permet de gérer le cycle de vie des données en mettant à jour ou en purgeant des enregistrements obsolètes ou inexacts.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 100%

---

# Hygiène de données sur Adobe Experience Platform

>[!IMPORTANT]
>
>L’hygiène des données n’est actuellement disponible que pour les organisations qui ont acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**.

Adobe Experience Platform offre un ensemble d’outils fiables pour gérer des opérations de données complexes et volumineuses afin d’orchestrer les expériences client. Les données étant ingérées dans le système au fil du temps, il devient de plus en plus important de gérer les banques de données pour que les données soient utilisées comme prévu, mises à jour lorsque des données incorrectes doivent être corrigées et supprimées lorsque les politiques d’entreprise le jugent nécessaire.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Ces activités peuvent être exécutées à l’aide de l’espace de travail de l’interface utilisateur [[!UICONTROL Hygiène des données]](#ui) ou de l’[API Data Hygiene](#api). Lorsqu’une tâche d’hygiène des données s’exécute, le système fournit des mises à jour de transparence à chaque étape du processus. Pour plus d’informations sur la représentation de chaque type de traitement dans le système, consultez la section sur [la chronologie et la transparence](#timelines-and-transparency).

## Espace de travail de l’interface utilisateur [!UICONTROL Nettoyage de données] {#ui}

L’espace de travail [!UICONTROL Hygiène des données] de l’interface utilisateur de Platform vous permet de configurer et de planifier des opérations de nettoyage de données et de vérifier que les enregistrements sont conservés comme prévu.

Pour obtenir des instructions détaillées sur la gestion des tâches de nettoyage de données dans l’interface utilisateur, consultez le [Guide de l’interface utilisateur de nettoyage de données](./ui/overview.md).

## API Data Hygiene {#api}

L’interface utilisateur [!UICONTROL Nettoyage de données] repose sur l’API Data Hygiene, dont vous pouvez utiliser les points d’entrée directement si vous préférez automatiser les activités de nettoyage de données. Pour plus d’informations, consultez le [Guide de l’API Data Hygiene](./api/overview.md).

## Chronologie et transparence

Les requêtes de suppression d’enregistrements et d’expiration de jeux de données disposent chacune de leur propre chronologie de traitement et fournissent des mises à jour de transparence à des points clés de leurs workflows respectifs.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Ce qui suit se produit lorsqu’une [requête d’expiration de jeu de données](./ui/dataset-expiration.md) est créée :

| Étape | Durée après expiration planifiée | Description |
| --- | --- | --- |
| La requête a été soumise | 0 heure | Un gestionnaire de données ou un analyste de la confidentialité soumet une requête pour qu’un jeu de données arrive à expiration à un moment donné. La requête est visible dans l’[!UICONTROL interface utilisateur de l’hygiène des données] après avoir été soumise, et reste dans un statut en attente jusqu’à l’heure d’expiration planifiée, après quoi la requête s’exécutera. |
| Jeu de données déposé | 1 heure | Le jeu de données est supprimé de la [page d’inventaire du jeu de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur. Les données du lac de données sont uniquement supprimées de manière réversible et le resteront jusqu’à la fin du processus, après quoi elles seront supprimées définitivement. |
| Nombre de profils mis à jour | 30 heures | Selon le contenu du jeu de données supprimé, certains profils peuvent être supprimés du système si tous leurs attributs de composant sont liés à ce jeu de données. 30 heures après la suppression du jeu de données, toutes les modifications résultantes dans le nombre total de profils sont répercutées dans les [widgets du tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Segments mis à jour | 48 heures | Une fois tous les profils affectés mis à jour, tous les [segments](../segmentation/home.md) connexes sont mis à jour pour refléter leur nouvelle taille. Selon le jeu de données supprimé et les attributs que vous segmentez, la taille de chaque segment peut augmenter ou diminuer en raison de la suppression. |
| Destinations et parcours mis à jour | 50 heures | Les [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=fr), [destinations](../destinations/home.md), et [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=fr) sont mis à jour en fonction des modifications apportées aux segments connexes. |
| Suppression définitive terminée | 14 jours | Toutes les données relatives au jeu de données sont supprimées définitivement du lac de données. Le [statut du traitement d’hygiène](./ui/browse.md#view-details) qui a supprimé le jeu de données est mis à jour pour refléter cette situation. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Étapes suivantes

Ce document présente une vue d’ensemble des fonctionnalités d’hygiène des données de Platform. Pour commencer à effectuer des demandes d’hygiène des données dans l’interface utilisateur, reportez-vous au [guide de l’interface utilisateur](./ui/overview.md). Pour savoir comment créer des traitements d’hygiène des données par programmation, reportez-vous au [guide de l’API Data Hygiene](./api/overview.md).
