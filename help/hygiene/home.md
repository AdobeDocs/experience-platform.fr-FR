---
title: Présentation de l’hygiène de données
description: Le nettoyage de données d’Adobe Experience Platform vous permet de gérer le cycle de vie des données en mettant à jour ou en purgeant des enregistrements obsolètes ou inexacts.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 70a2abcc4d6e27a89e77d68e7757e4876eaa4fc0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 72%

---

# Hygiène de données sur Adobe Experience Platform

>[!IMPORTANT]
>
>L’hygiène des données n’est actuellement disponible que pour les organisations qui ont acheté **Adobe Health Care Shield** ou **Adobe de la confidentialité et de la sécurité**.

Adobe Experience Platform offre un ensemble d’outils fiables pour gérer des opérations de données complexes et volumineuses afin d’orchestrer les expériences client. Les données étant ingérées dans le système au fil du temps, il devient de plus en plus important de gérer les banques de données pour que les données soient utilisées comme prévu, mises à jour lorsque des données incorrectes doivent être corrigées et supprimées lorsque les politiques d’entreprise le jugent nécessaire.

Les fonctionnalités d’hygiène des données de Platform vous permettent de gérer vos données stockées par le biais des éléments suivants :

* Planifier l’expiration automatisée des jeux de données
* Suppression d’enregistrements individuels d’un ou de tous les jeux de données

>[!IMPORTANT]
>
>Les suppressions d’enregistrements sont destinées à être utilisées pour la normalisation des données, la suppression des données anonymes ou la minimisation des données. Ils sont **not** à utiliser pour les demandes de droits des titulaires de données (conformité) en ce qui concerne les réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD). Pour tous les cas d’utilisation de conformité, utilisez [Adobe Experience Platform Privacy Service](../privacy-service/home.md) au lieu de .

Ces activités peuvent être exécutées à l’aide de l’espace de travail de l’interface utilisateur [[!UICONTROL Hygiène des données]](#ui) ou de l’[API Data Hygiene](#api). Lorsqu’une tâche d’hygiène des données s’exécute, le système fournit des mises à jour de transparence à chaque étape du processus. Pour plus d’informations sur la représentation de chaque type de traitement dans le système, consultez la section sur [la chronologie et la transparence](#timelines-and-transparency).

## Espace de travail de l’interface utilisateur [!UICONTROL Nettoyage de données] {#ui}

L’espace de travail [!UICONTROL Hygiène des données] de l’interface utilisateur de Platform vous permet de configurer et de planifier des opérations de nettoyage de données et de vérifier que les enregistrements sont conservés comme prévu.

Pour obtenir des instructions détaillées sur la gestion des tâches de nettoyage de données dans l’interface utilisateur, consultez le [Guide de l’interface utilisateur de nettoyage de données](./ui/overview.md).

## API Data Hygiene {#api}

L’interface utilisateur [!UICONTROL Nettoyage de données] repose sur l’API Data Hygiene, dont vous pouvez utiliser les points d’entrée directement si vous préférez automatiser les activités de nettoyage de données. Pour plus d’informations, consultez le [Guide de l’API Data Hygiene](./api/overview.md).

## Chronologie et transparence

Les demandes de suppression et d’expiration de jeux de données d’enregistrement ont chacune leur propre chronologie de traitement et fournissent des mises à jour de transparence à des points clés de leurs workflows respectifs. Reportez-vous aux sections ci-dessous pour plus d’informations sur chaque type de traitement.

### Expirations de jeux de données {#dataset-expiration-transparency}

Ce qui suit se produit lorsqu’une [requête d’expiration de jeu de données](./ui/dataset-expiration.md) est créée :

| Étape | Durée après expiration planifiée | Description |
| --- | --- | --- |
| La requête a été soumise | 0 heure | Un gestionnaire de données ou un analyste de la confidentialité soumet une requête pour qu’un jeu de données arrive à expiration à un moment donné. La requête est visible dans l’[!UICONTROL interface utilisateur de l’hygiène des données] après avoir été soumise, et reste dans un statut en attente jusqu’à l’heure d’expiration planifiée, après quoi la requête s’exécutera. |
| Jeu de données déposé | 1 heure | Le jeu de données est supprimé de la [page d’inventaire du jeu de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur. Les données du lac de données sont uniquement supprimées de manière réversible et le resteront jusqu’à la fin du processus, après quoi elles seront supprimées définitivement. |
| Nombre de profils mis à jour | 30 heures | Selon le contenu du jeu de données supprimé, certains profils peuvent être supprimés du système si tous leurs attributs de composant sont liés à ce jeu de données. 30 heures après la suppression du jeu de données, toutes les modifications résultantes dans le nombre total de profils sont répercutées dans [widgets de tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Segments mis à jour | 48 heures | Une fois tous les profils concernés mis à jour, tous les profils associés [segments](../segmentation/home.md) sont mises à jour pour refléter leur nouvelle taille. Selon le jeu de données supprimé et les attributs sur lesquels vous segmentez, la taille de chaque segment peut augmenter ou diminuer en raison de la suppression. |
| Destinations et parcours mis à jour | 50 heures | Les [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=fr), [destinations](../destinations/home.md), et [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=fr) sont mis à jour en fonction des modifications apportées aux segments connexes. |
| Suppression définitive terminée | 14 jours | Toutes les données relatives au jeu de données sont supprimées définitivement du lac de données. Le [statut du traitement d’hygiène](./ui/browse.md#view-details) qui a supprimé le jeu de données est mis à jour pour refléter cette situation. |

{style=&quot;table-layout:auto&quot;}

### Suppressions d’enregistrements {#record-delete-transparency}

>[!IMPORTANT]
>
>Les suppressions de dossiers ne sont disponibles que pour les organisations qui ont acheté Adobe Healthcare Shield.

Ce qui suit se produit lorsqu’une [requête de suppression d’enregistrement](./ui/record-delete.md) est créé :

| Étape | Durée après soumission de la requête | Description |
| --- | --- | --- |
| La requête a été soumise | 0 heure | Un gestionnaire de données ou un analyste de la confidentialité envoie une demande de suppression d’enregistrement. La requête est visible dans l’[!UICONTROL interface utilisateur de l’hygiène des données] après avoir été soumise. |
| Mises à jour des recherches de profil | 3 heures | Les modifications du nombre de profils provoquées par l’identité supprimée sont appliquées dans les [widgets de tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Segments mis à jour | 24 heures | Une fois les profils supprimés, tous les [segments](../segmentation/home.md) connexes sont mis à jour pour refléter leur nouvelle taille. |
| Destinations et parcours mis à jour | 26 heures | [Campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), [destinations](../destinations/home.md) et [parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html) sont mis à jour en fonction des modifications apportées aux segments connexes. |
| Enregistrements supprimés de manière réversible dans le lac de données | 7 jours | Les données sont supprimées de manière réversible du lac de données. |
| Aspiration des données terminée | 14 jours | Le [statut du traitement d’hygiène](./ui/browse.md#view-details) se met à jour pour indiquer que le traitement est terminé, ce qui signifie que l’aspiration de données est achevée dans le lac de données et que les enregistrements pertinents ont été définitivement supprimés. |

{style=&quot;table-layout:auto&quot;}

## Étapes suivantes

Ce document présente une vue d’ensemble des fonctionnalités d’hygiène des données de Platform. Pour commencer à effectuer des demandes d’hygiène des données dans l’interface utilisateur, reportez-vous au [guide de l’interface utilisateur](./ui/overview.md). Pour savoir comment créer des traitements d’hygiène des données par programmation, reportez-vous au [guide de l’API Data Hygiene](./api/overview.md).
