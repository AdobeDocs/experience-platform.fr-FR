---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Règles d’alerte standard
description: Ce document couvre les règles d’alerte prédéfinies fournies par Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 17%

---

# Règles d’alerte standard

Adobe Experience Platform fournit plusieurs règles d’alerte prédéfinies que vous pouvez activer pour votre organisation. Le tableau ci-dessous présente les détails de ces règles d’alerte fournies par l’Adobe. Pour plus d’informations sur les alertes en Experience Platform, consultez la [présentation des alertes](./overview.md).

| Composants de  | Description | Fréquence d&#39;évaluation | Fenêtre de répétition |
| --- | --- | --- | --- |
| Succès de l’exécution du flux de sources | Cette alerte se déclenche lorsque les données sont correctement ingérées à partir d’une connexion source. | S.O. | S.O. |
| Échec de l’exécution du flux des sources | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données à partir d’une connexion source. | S.O. | S.O. |
| Délai de tâche de segment | Cette alerte se déclenche lorsqu’une tâche de segmentation prend plus de 150 minutes. | 30 secondes | 3 heures |
| Définition de segment désactivée | Cette alerte se déclenche lorsqu’une définition de segment est désactivée. | S.O. | N/A |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
