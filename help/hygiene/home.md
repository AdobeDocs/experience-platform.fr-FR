---
title: Présentation de l’hygiène des données
description: Le nettoyage de données d’Adobe Experience Platform vous permet de gérer le cycle de vie des données en mettant à jour ou en purgeant des enregistrements obsolètes ou inexacts.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 51181dccbd37df60e438f34090ebaeb9e327c4ce
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 26%

---

# Veille des données dans Adobe Experience Platform

Adobe Experience Platform offre un ensemble d’outils fiables pour gérer des opérations de données complexes et volumineuses afin d’orchestrer les expériences client. Les données étant ingérées dans le système au fil du temps, il devient de plus en plus important de gérer les banques de données pour que les données soient utilisées comme prévu, mises à jour lorsque des données incorrectes doivent être corrigées et supprimées lorsque les politiques d’entreprise le jugent nécessaire.

Les fonctionnalités d’hygiène des données de Platform vous permettent de gérer vos données client stockées par le biais des éléments suivants :

* Planification de l’expiration automatisée des jeux de données
* Suppression des données des consommateurs en fonction des identités ingérées

>[!NOTE]
>
>Les demandes de suppression des consommateurs ne sont disponibles que pour les organisations qui ont acheté Adobe Healthcare Shield ou Privacy Shield.

Ces activités peuvent être exécutées à l’aide du [[!UICONTROL Hygiène des données] Espace de travail de l’interface utilisateur](#ui) ou le [API Data Hygiene](#api). Lorsqu’une tâche d’hygiène des données s’exécute, le système fournit des mises à jour de transparence à chaque étape du processus. Voir la section sur [calendrier et transparence](#timelines-and-transparency) pour plus d’informations sur la représentation de chaque type de tâche dans le système.

## Espace de travail de l’interface utilisateur [!UICONTROL Nettoyage de données] {#ui}

L’espace de travail [!UICONTROL Hygiène des données] de l’interface utilisateur de Platform vous permet de configurer et de planifier des opérations de nettoyage de données et de vérifier que les enregistrements sont conservés comme prévu.

Pour obtenir des instructions détaillées sur la gestion des tâches de nettoyage de données dans l’interface utilisateur, consultez le [Guide de l’interface utilisateur de nettoyage de données](./ui/overview.md).

## API Data Hygiene {#api}

L’interface utilisateur [!UICONTROL Nettoyage de données] repose sur l’API Data Hygiene, dont vous pouvez utiliser les points d’entrée directement si vous préférez automatiser les activités de nettoyage de données. Pour plus d’informations, consultez le [Guide de l’API Data Hygiene](./api/overview.md).

## Chronologies et transparence

Les demandes de suppression et d’expiration de jeux de données des clients disposent chacune de leurs propres chronologies de traitement et fournissent des mises à jour de transparence à des points clés de leurs workflows respectifs. Reportez-vous aux sections ci-dessous pour plus d’informations sur chaque type de tâche.

### Expirations de jeux de données {#dataset-expiration-transparency}

Ce qui suit se produit lorsqu’une [demande d’expiration du jeu de données](./ui/dataset-expiration.md) est créé :

| Évaluation | Durée après expiration planifiée | Description |
| --- | --- | --- |
| La demande est envoyée | 0 heures | Un gestionnaire de données ou un analyste de la confidentialité envoie une demande pour qu’un jeu de données arrive à expiration à un moment donné. La requête est visible dans la variable [!UICONTROL Interface utilisateur de l’hygiène des données] une fois qu’il a été envoyé et reste dans un état en attente jusqu’à l’heure d’expiration planifiée, après laquelle la demande s’exécutera. |
| Jeu de données déposé | 1 heure | Le jeu de données est supprimé de la variable [page d’inventaire du jeu de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur. Les données du lac de données ne sont supprimées de manière réversible que jusqu’à la fin du processus, après quoi elles seront supprimées de manière irréversible. |
| Nombre de profils mis à jour | 30 heures | La modification du nombre de profils provoquée par l’expiration du jeu de données est répercutée dans [widgets de tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Segments mis à jour | 48 heures | Une fois les profils supprimés, tous les [segments](../segmentation/home.md) sont mises à jour pour refléter leur nouvelle taille. |
| Parcours et destinations mis à jour | 50 heures | [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), et [destinations](../destinations/home.md) sont mises à jour en fonction des modifications apportées aux segments connexes. |
| Fin de la suppression définitive | 14 jours | Toutes les données relatives au jeu de données sont fortement supprimées du lac de données. Le [statut de l&#39;hygiène](./ui/browse.md#view-details) qui a supprimé le jeu de données est mis à jour pour refléter cette situation. |

{style=&quot;table-layout:auto&quot;}

### Suppressions des consommateurs {#consumer-delete-transparency}

Ce qui suit se produit lorsqu’une [requête de suppression du client](./ui/delete-consumer.md) est créé :

| Évaluation | Durée après envoi de la requête | Description |
| --- | --- | --- |
| La demande est envoyée | 0 heures | Un gestionnaire de données ou un analyste de la confidentialité envoie une demande de suppression de consommateur. La requête est visible dans la variable [!UICONTROL Interface utilisateur de l’hygiène des données] après avoir été soumis. |
| Mises à jour des recherches de profil | 3 heures | La modification du nombre de profils provoquée par l’identité supprimée est répercutée dans [widgets de tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Segments mis à jour | 24 heures | Une fois les profils supprimés, tous les [segments](../segmentation/home.md) sont mises à jour pour refléter leur nouvelle taille. |
| Parcours et destinations mis à jour | 26 heures | [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), et [destinations](../destinations/home.md) sont mises à jour en fonction des modifications apportées aux segments connexes. |
| Enregistrements supprimés en douceur dans le lac de données | 7 jours | Les données sont supprimées de manière réversible du lac de données. |
| Passage des données terminé | 14 jours | Le [statut de l&#39;hygiène](./ui/browse.md#view-details) mises à jour pour indiquer que la tâche est terminée, ce qui signifie que l’aspirateur de données a été terminé sur le lac de données et que les enregistrements pertinents ont été définitivement supprimés. |

{style=&quot;table-layout:auto&quot;}

## Étapes suivantes

Ce document présente les fonctionnalités d’hygiène des données de Platform. Pour commencer à effectuer des demandes d’hygiène des données dans l’interface utilisateur, reportez-vous à la section [Guide de l’interface utilisateur](./ui/overview.md). Pour savoir comment créer des tâches d’hygiène des données par programmation, reportez-vous à la section [Guide de l’API d’hygiène des données](./api/overview.md)
