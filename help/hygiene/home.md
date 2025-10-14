---
title: Présentation De La Gestion Avancée Du Cycle De Vie Des Données
description: La gestion avancée du cycle de vie des données vous permet de gérer le cycle de vie des données en mettant à jour ou en purgeant des enregistrements obsolètes ou inexacts.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 9ffd2db5555a4c157171d488deb9641aadbb08b4
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 33%

---

# Gestion avancée du cycle de vie des données dans Adobe Experience Platform

Adobe Experience Platform offre un ensemble d’outils fiables pour gérer des opérations de données complexes et volumineuses afin d’orchestrer les expériences client. Les données étant ingérées dans le système au fil du temps, il devient de plus en plus important de gérer les banques de données pour que les données soient utilisées comme prévu, mises à jour lorsque des données incorrectes doivent être corrigées et supprimées lorsque les politiques d’entreprise le jugent nécessaire.

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Ces activités peuvent être effectuées à l’aide de l’espace de travail de l’interface utilisateur [[!UICONTROL cycle de vie des données] &#x200B;](#ui) ou de l’API [Data Hygiene](#api). Lorsqu’une tâche du cycle de vie des données s’exécute, le système fournit des mises à jour de transparence à chaque étape du processus. Pour plus d’informations sur la représentation de chaque type de traitement dans le système, consultez la section sur [la chronologie et la transparence](#timelines-and-transparency).

>[!NOTE]
>
>Advanced Data Lifecycle Management prend en charge les suppressions de jeux de données via le [point d’entrée d’expiration du jeu de données](./api/dataset-expiration.md) et les suppressions d’identifiants (données au niveau des lignes) à l’aide d’identités principales via le [point d’entrée d’ordre de travail](./api/workorder.md). Vous pouvez également gérer les [expirations de jeux de données](./ui/dataset-expiration.md) et [suppressions d’enregistrements](./ui/record-delete.md) via l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez la documentation associée . Notez que le cycle de vie des données ne prend pas en charge la suppression de lots.

## Espace de travail de l’interface utilisateur [!UICONTROL cycle de vie des données] {#ui}

L’espace de travail [!UICONTROL Cycle de vie des données] de l’interface utilisateur d’Experience Platform vous permet de configurer et de planifier des opérations de cycle de vie des données et de vous assurer que les enregistrements sont conservés comme prévu.

Pour obtenir des instructions détaillées sur la gestion des tâches du cycle de vie des données dans l’interface utilisateur, consultez le [guide de l’interface utilisateur du cycle de vie des données](./ui/overview.md).

## API Data Hygiene {#api}

L’interface utilisateur [!UICONTROL Cycle de vie des données] repose sur l’API Data Hygiene, dont vous pouvez utiliser les points d’entrée directement si vous préférez automatiser les activités de cycle de vie des données. Pour plus d’informations, consultez le [Guide de l’API Data Hygiene](./api/overview.md).

## Chronologie et transparence {#timelines-and-transparency}

Les demandes [suppression d’enregistrements](./ui/record-delete.md) et d’expiration de jeu de données ont chacune leur propre chronologie de traitement et fournissent des mises à jour de transparence à des points clés de leurs workflows respectifs.

>[!TIP]
>
>Pour surveiller votre utilisation actuelle par rapport aux limites de quota, consultez le [Guide de référence des quotas](./api/quota.md).\
>Pour les règles de droits, les limites mensuelles, la chronologie SLA et les politiques de gestion des exceptions, consultez la documentation [Suppression d’enregistrements (IU)](./ui/record-delete.md#quotas) et [Ordre de travail (API)](./api/workorder.md#quotas).

Ce qui suit se produit lorsqu’une [requête d’expiration de jeu de données](./ui/dataset-expiration.md) est créée :

| Étape | Durée après expiration planifiée | Description |
| --- | --- | --- |
| La requête a été soumise | 0 heure | Un gestionnaire de données ou un analyste de la confidentialité soumet une demande pour qu’un jeu de données expire à un moment donné. La requête est visible dans l’[!UICONTROL interface utilisateur du cycle de vie des données] après avoir été soumise, et reste dans un statut en attente jusqu’à l’heure d’expiration planifiée, après quoi la requête s’exécutera. |
| Le jeu de données est marqué pour suppression | 0-2 heures | Une fois la requête exécutée, le jeu de données est marqué pour suppression. Si vous utilisez le stockage de données Amazon Web Services (AWS), ce processus peut prendre jusqu’à deux heures. Pendant ce temps, les opérations telles que la segmentation par lots et en flux continu, la prévisualisation ou l’estimation, l’exportation et l’accès ignorent ce jeu de données. |
| Jeu de données déposé | 3 heures | **Une heure après que le jeu de données est marqué pour suppression**, il est entièrement supprimé du système. À ce stade, le jeu de données est supprimé de la [page d’inventaire des jeux de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur. Toutefois, les données du lac de données ne sont que supprimées de manière réversible à ce stade et le resteront jusqu’à ce que le processus de suppression définitive soit terminé. |
| Nombre de profils mis à jour | 30 heures | Selon le contenu du jeu de données supprimé, certains profils peuvent être supprimés du système si tous leurs attributs de composant sont liés à ce jeu de données. 30 heures après la suppression du jeu de données, toutes les modifications résultantes dans le nombre total de profils sont répercutées dans les [widgets du tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Audiences mises à jour | 48 heures | Une fois tous les profils affectés mis à jour, toutes les [audiences](../segmentation/home.md) connexes sont mises à jour pour refléter leur nouvelle taille. Selon le jeu de données supprimé et les attributs que vous segmentez, la taille de chaque audience peut augmenter ou diminuer en raison de la suppression. |
| Destinations et parcours mis à jour | 50 heures | Les [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=fr), [destinations](../destinations/home.md), et [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=fr) sont mis à jour en fonction des modifications apportées aux segments connexes. |
| Suppression définitive terminée | 15 jours | Toutes les données relatives au jeu de données sont supprimées définitivement du lac de données. Le [statut de la tâche du cycle de vie des données](./ui/browse.md#view-details) qui a supprimé le jeu de données est mis à jour pour refléter cette situation. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Les suppressions de jeux de données dans Amazon Web Services (AWS) sont soumises à une latence d’environ trois heures avant que les modifications ne soient entièrement appliquées. Cela inclut jusqu’à deux heures pour que le jeu de données soit marqué pour suppression, suivies d’une heure supplémentaire avant qu’il ne soit complètement supprimé du système. En revanche, les demandes de suppression d’instances Experience Platform qui utilisent Azure Data Lake entraînent des modifications immédiates dans toutes les fonctions commerciales.
>
>Pour les utilisateurs AWS, ce délai peut avoir un impact sur la segmentation par lots, la segmentation par flux, les aperçus, les estimations, les exportations et l’accès aux données. Cette latence affecte uniquement les clients qui utilisent AWS, car les utilisateurs d’Azure Data Lake bénéficient de mises à jour immédiates. Pour les utilisateurs d’AWS, les demandes de suppression peuvent prendre jusqu’à trois heures pour se propager entièrement sur tous les systèmes affectés. Ajustez vos attentes en conséquence.


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=fr), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=fr), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Étapes suivantes

Ce document présente un aperçu des fonctionnalités d’Experience Platform relatives au cycle de vie des données. Pour commencer à effectuer des demandes d’hygiène des données dans l’interface utilisateur, reportez-vous au [guide de l’interface utilisateur](./ui/overview.md). Pour savoir comment créer des tâches de cycle de vie des données par programmation, reportez-vous au guide de l’API [&#x200B; Data Hygiene &#x200B;](./api/overview.md)
