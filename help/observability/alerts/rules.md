---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Règles d’alerte standard
description: Ce document couvre les règles d’alerte prédéfinies fournies par Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d8ada2de0ee0408e4e10f0dc45652af6eb6352cf
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 16%

---

# Règles d’alerte standard

Adobe Experience Platform fournit plusieurs règles d’alerte prédéfinies que vous pouvez activer pour votre organisation. Ce document couvre les détails de ces règles d’alerte fournies par l’Adobe. Pour plus d’informations sur les alertes dans Experience Platform, consultez la [présentation des alertes](./overview.md).

When [affichage des règles d’alerte dans l’interface utilisateur de Platform](./ui.md), vous pouvez vous abonner à chaque règle individuellement. Lorsque vous vous abonnez à des alertes par le biais de [Notifications d’événements d’E/S](./subscribe.md), toutefois, les règles d’alerte sont organisées en différents packages d’abonnement. Dans les tableaux ci-dessous, chaque règle est affichée avec son nom d’abonnement d’événement d’E/S correspondant.

## Ingestion de données

Les règles d’alerte suivantes sont spécifiques à [Ingestion des données](../../ingestion/home.md) et  [sources](../../sources/home.md):

| abonnement aux événements I/O | Règle d&#39;alerte | Description |
| --- | --- | --- |
| Informations sur l’exécution du flux source | Démarrage de l’exécution du flux de sources | Cette alerte se déclenche lorsqu’une connexion source commence le traitement des données. |
| Informations sur l’exécution du flux source | Succès de l’exécution du flux de sources | Cette alerte se déclenche lorsque les données sont correctement ingérées à partir d’une connexion source. |
| Retards, échecs et erreurs d’exécution de flux source | Échec de l’exécution du flux des sources | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données à partir d’une connexion source. |
| Retards, échecs et erreurs d’exécution de flux source | Délai d’ingestion | Cette alerte se déclenche lorsqu’une exécution du flux d’ingestion par lots dure plus de 150 minutes. |

{style=&quot;table-layout:auto&quot;}

## Identity Service

Les règles d’alerte suivantes sont spécifiques à [Identity Service](../../identity-service/home.md):

| abonnement aux événements I/O | Règle d&#39;alerte | Description |
| --- | --- | --- |
| Informations sur l’ingestion d’identités | Démarrage de l’exécution du flux Identity Service | Cette alerte se déclenche lorsqu’une exécution de flux Identity Service démarre le traitement des données. En d’autres termes, les données ingérées sont chargées du lac de données vers Identity Service. |
| Informations sur l’ingestion d’identités | Succès de l’exécution du flux Identity Service | Cette alerte se déclenche lorsque les données sont correctement chargées du lac de données vers Identity Service. |
| Retards, échecs et erreurs d’ingestion d’identités | Délai d’exécution du flux Identity Service | Cette alerte se déclenche lorsqu’une exécution de flux Identity Service prend plus de 150 minutes pour être traitée. |
| Retards, échecs et erreurs d’ingestion d’identités | Échec de l’exécution du flux Identity Service | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données dans Identity Service. |

{style=&quot;table-layout:auto&quot;}

## Real-time Customer Profile

Les règles d’alerte suivantes sont spécifiques à [Real-time Customer Profile](../../profile/home.md):

| abonnement aux événements I/O | Règle d&#39;alerte | Description |
| --- | --- | --- |
| Informations sur l’ingestion du profil | Démarrage de l’exécution du flux de profil | Cette alerte se déclenche lorsqu’une exécution de flux de profil démarre le traitement des données. |
| Informations sur l’ingestion du profil | Succès de l’exécution du flux de profil | Cette alerte se déclenche lorsque les données sont chargées correctement dans Profile à partir du lac de données. |
| Retards, échecs et erreurs d’ingestion du profil | Délai d’exécution du flux de profil | Cette alerte se déclenche lors du chargement des données du lac de données dans Profile pendant plus de 150 minutes. |
| Retards, échecs et erreurs d’ingestion du profil | Échec de l’exécution du flux de profil | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données dans Profile. |

{style=&quot;table-layout:auto&quot;}

## Segmentation

Les règles d’alerte suivantes sont spécifiques à [Segmentation Service](../../segmentation/home.md):

| abonnement aux événements I/O | Règle d&#39;alerte | Description |
| --- | --- | --- |
| Informations sur la tâche d’évaluation de segment | Démarrage de la tâche de segment | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segment commence à traiter des données. |
| Informations sur la tâche d’évaluation de segment | Réussite de la tâche de segment | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segment se termine avec succès. |
| Retards, échecs et erreurs de tâche d’évaluation de segment | Délai de tâche de segmentation | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segment dure plus de 150 minutes. |
| Retards, échecs et erreurs de tâche d’évaluation de segment | Échec de la tâche de segment | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segment génère une erreur. |
| Retards, échecs et erreurs de tâche d’évaluation de segment | Définition de segment désactivée | Cette alerte se déclenche lorsqu’une définition de segment est désactivée en raison d’une erreur interne. Cela déclenche automatiquement une salle de guerre pour qu&#39;une équipe d&#39;ingénierie d&#39;Adobe enquête sur le problème. Cette alerte a pour seul but d’être informative et ne nécessite aucune action de votre part. |

{style=&quot;table-layout:auto&quot;}

## Destinations

Les règles d’alerte suivantes sont spécifiques à [destinations](../../destinations/home.md):

| abonnement aux événements I/O | Règle d&#39;alerte | Description |
| --- | --- | --- |
| Informations sur l’exécution du flux de destination | Démarrage de l’exécution du flux de destination | Cette alerte se déclenche lorsqu’une exécution de flux de destination commence à activer un segment. |
| Informations sur l’exécution du flux de destination | Succès de l’exécution du flux de destination | Cette alerte se déclenche lorsqu’un segment est activé avec succès vers une destination. |
| Délais, échecs et erreurs d’exécution du flux de destination | Délai d’exécution du flux de destination | Cette alerte se déclenche lorsqu’une exécution de flux de destination dure plus de 150 minutes pour activer un segment. |
| Délais, échecs et erreurs d’exécution du flux de destination | Échec de l’exécution du flux de destination | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’activation d’un segment vers une destination. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
