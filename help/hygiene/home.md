---
title: Présentation De La Gestion Avancée Du Cycle De Vie Des Données
description: La gestion avancée du cycle de vie des données vous permet de gérer le cycle de vie des données en mettant à jour ou en purgeant des enregistrements obsolètes ou inexacts.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: adba9d3cd979f655f477d2d80ed3e55e96fbe486
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 21%

---

# Gestion avancée du cycle de vie des données dans Adobe Experience Platform

Adobe Experience Platform offre un ensemble d’outils fiables pour gérer des opérations de données complexes et volumineuses afin d’orchestrer les expériences client. Les données étant ingérées dans le système au fil du temps, il devient de plus en plus important de gérer les banques de données pour que les données soient utilisées comme prévu, mises à jour lorsque des données incorrectes doivent être corrigées et supprimées lorsque les politiques d’entreprise le jugent nécessaire.

Ces activités peuvent être effectuées à l’aide de l’espace de travail de l’interface utilisateur [[!UICONTROL Data Lifecycle] ](#ui) ou de l’[API Data Hygiene](#api). Lorsqu’une tâche du cycle de vie des données s’exécute, le système fournit des mises à jour de transparence à chaque étape du processus. Pour plus d’informations sur la représentation de chaque type de traitement dans le système, consultez la section sur [la chronologie et la transparence](#timelines-and-transparency).

>[!NOTE]
>
>Advanced Data Lifecycle Management prend en charge les suppressions de jeux de données via le [point d’entrée d’expiration du jeu de données](./api/dataset-expiration.md) et les suppressions d’identifiants (données au niveau des lignes) à l’aide d’identités principales via le [point d’entrée d’ordre de travail](./api/workorder.md). Vous pouvez également gérer les [expirations de jeux de données](./ui/dataset-expiration.md) et [suppressions d’enregistrements](./ui/record-delete.md) via l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez la documentation associée . Notez que le cycle de vie des données ne prend pas en charge la suppression de lots.

## Espace de travail de l’interface utilisateur [!UICONTROL Data Lifecycle] {#ui}

L’espace de travail [!UICONTROL Data Lifecycle] de l’interface utilisateur d’Experience Platform vous permet de configurer et de planifier des opérations de cycle de vie des données et de vous assurer que les enregistrements sont conservés comme prévu.

Pour obtenir des instructions détaillées sur la gestion des tâches du cycle de vie des données dans l’interface utilisateur, consultez le [guide de l’interface utilisateur du cycle de vie des données](./ui/overview.md).

## API Data Hygiene {#api}

L’interface utilisateur de [!UICONTROL Data Lifecycle] repose sur l’API Data Hygiene, dont vous pouvez utiliser les points d’entrée directement si vous préférez automatiser les activités du cycle de vie des données. Pour plus d’informations, consultez le [Guide de l’API Data Hygiene](./api/overview.md).

## Chronologie et transparence {#timelines-and-transparency}

Les demandes [suppression d’enregistrements](./ui/record-delete.md) et d’expiration de jeu de données ont chacune leur propre chronologie de traitement et fournissent des mises à jour de transparence à des points clés de leurs workflows respectifs.

>[!TIP]
>
>Pour plus d’informations de référence :
>- Pour surveiller votre utilisation actuelle par rapport aux limites de quota, consultez le [Guide de référence des quotas](./api/quota.md).
>- Pour les règles de droits, les limites mensuelles, la chronologie SLA et les politiques de gestion des exceptions, consultez les guides [ Guide du quota de suppression d’enregistrements (IU)](./ui/record-delete.md#quotas) et [ Guide du quota d’ordres de travail (API)](./api/workorder.md#quotas).

Ce qui suit se produit lorsqu’une [requête d’expiration de jeu de données](./ui/dataset-expiration.md) est créée :

| Étape | Durée après expiration planifiée | Description |
| --- | --- | --- |
| La requête a été soumise | 0 heure | Un gestionnaire de données ou un analyste de la confidentialité soumet une demande pour qu’un jeu de données expire à un moment donné. La requête est visible dans le [!UICONTROL Data Lifecycle UI] après avoir été soumise et reste dans un statut en attente jusqu’à l’heure d’expiration planifiée, après quoi la requête s’exécutera. |
| Jeu de données supprimé du lac de données | 1 heure | Le jeu de données est supprimé de la page d’inventaire [jeu de données](../catalog/datasets/user-guide.md) dans l’interface utilisateur. Les données du lac de données sont uniquement supprimées de manière réversible et le resteront jusqu’à la fin du processus, après quoi elles seront supprimées définitivement. |
| Jeu de données supprimé du service de profil | 3 heures | À partir de maintenant, les opérations comprenant la segmentation par lots et en flux continu, la prévisualisation ou l’estimation, l’exportation et l’accès aux entités ne liront plus les données de ce jeu de données. Les données du service de profil sont uniquement supprimées de manière réversible et le resteront jusqu’à la fin du processus, après quoi elles seront supprimées définitivement. |
| Nombre de profils et audiences mis à jour | 48 heures | Une fois tous les profils affectés mis à jour, toutes les [audiences](../segmentation/home.md) connexes sont mises à jour pour refléter leur nouvelle taille. Selon le jeu de données supprimé et les attributs que vous segmentez, la taille de chaque audience peut augmenter ou diminuer en raison de la suppression. À ce stade, toutes les modifications résultantes dans le nombre total de profils sont répercutées dans les [widgets de tableau de bord](../dashboards/guides/profiles.md#profile-count-trend) et d’autres rapports. |
| Destinations et parcours mis à jour | 50 heures | Les [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=fr), [destinations](../destinations/home.md), et [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=fr) sont mis à jour en fonction des modifications apportées aux segments connexes. |
| Suppression définitive terminée | 15 jours | Toutes les données liées au jeu de données sont supprimées définitivement du lac de données et du service de profil. Le [statut de la tâche du cycle de vie des données](./ui/browse.md#view-details) qui a supprimé le jeu de données est mis à jour pour refléter cette situation. |

{style="table-layout:auto"}

### Chronologies de suppression des enregistrements {#record-delete-transparency}

Ce qui suit se produit après l’envoi d’une [demande de suppression d’enregistrement](./ui/record-delete.md).

>[!NOTE]
>
>Les durées sont approximatives et varient en fonction de la charge du système, de la planification par lots et du niveau de droits. Le SLA de bout en bout (30 jours standard, 15 jours pour Privacy and Security Shield ou Healthcare Shield) constitue l’engagement opérationnel.

| Étape | Env. synchronisation | Description |
| --- | --- | --- |
| Demande envoyée et groupée | Jour 1-15 | Un ordre de travail est créé et mis en file d’attente. Les demandes peuvent être mises en file d’attente et traitées par lots pendant 14 jours au maximum avant le début du traitement. Le traitement par lots est la principale raison pour laquelle la suppression n’est pas immédiate. |
| Les systèmes en aval traitent la demande de suppression | Jour 16-25 | Les services en aval reçoivent et exécutent la requête de suppression d’enregistrement. |
| Tampon — contrôles d&#39;intégrité et renvois | Jour 25-30 | Une fenêtre de mémoire tampon permet de vérifier l’intégrité et de soumettre à nouveau les tâches ayant échoué avant que la fenêtre SLA ne se ferme. Le statut de l’ordre de travail est mis à jour sur `completed` une fois que tous les systèmes confirment la suppression. |

{style="table-layout:auto"}

Pour les durées de file d’attente basées sur les droits et les valeurs SLA maximales, consultez [Traitement des chronologies pour les envois d’identifiants](./ui/record-delete.md#sla-processing-timelines).

## Étapes suivantes {#next-steps}

Ce document présente les fonctionnalités du cycle de vie des données d’Experience Platform. Pour commencer à effectuer des demandes d’hygiène des données dans l’interface utilisateur, consultez le [guide de l’interface utilisateur du cycle de vie des données](./ui/overview.md). Pour créer des tâches de cycle de vie des données par programmation, consultez le [ Guide de l’API Data Hygiene ](./api/overview.md).
