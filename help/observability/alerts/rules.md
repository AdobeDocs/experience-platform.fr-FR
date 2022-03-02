---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Règles d’alerte standard
description: Ce document couvre les règles d’alerte prédéfinies fournies par Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d8ada2de0ee0408e4e10f0dc45652af6eb6352cf
workflow-type: ht
source-wordcount: '728'
ht-degree: 100%

---

# Règles d’alerte standard

Adobe Experience Platform fournit plusieurs règles d’alerte prédéfinies que vous pouvez activer pour votre organisation. Ce document couvre les détails de ces règles d’alerte fournies par Adobe. Pour plus d’informations concernant les alertes dans Experience Platform, consultez la [présentation des alertes](./overview.md).

Lors de l’[affichage des règles d’alerte dans l’interface utilisateur de Platform](./ui.md), vous pouvez vous abonner à chaque règle. Toutefois, lorsque vous vous abonnez à des alertes par le biais des [Notifications d’événements I/O](./subscribe.md), les règles d’alerte sont organisées en différents packages d’abonnement. Dans les tableaux ci-dessous, chaque règle est affichée avec son nom d’abonnement aux événements I/O correspondant.

## Ingestion des données

Les règles d’alerte suivantes sont spécifiques à l’[Ingestion des données](../../ingestion/home.md) et aux [sources](../../sources/home.md) :

| Abonnement aux événements I/O | Règle d’alerte | Description |
| --- | --- | --- |
| Informations relatives à l’exécution du flux de sources | Début d’exécution du flux de sources | Cette alerte se déclenche lorsqu’une connexion source commence le traitement des données. |
| Informations relatives à l’exécution du flux de sources | Succès de l’exécution du flux de sources | Cette alerte se déclenche lorsque les données sont correctement ingérées à partir d’une connexion source. |
| Retards, échecs et erreurs de l’exécution du flux de sources | Échec de l’exécution du flux des sources | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données à partir d’une connexion source. |
| Retards, échecs et erreurs de l’exécution du flux de sources | Retard d’ingestion | Cette alerte se déclenche lorsqu’une exécution de flux d’ingestion par lots dure plus de 150 minutes. |

{style=&quot;table-layout:auto&quot;}

## Service d’identités

Les règles d’alerte suivantes sont spécifiques au [service d’identités](../../identity-service/home.md) :

| Abonnement aux événements I/O | Règle d’alerte | Description |
| --- | --- | --- |
| Informations relatives à l’ingestion d’identités | Début d’exécution du flux du service d’identités | Cette alerte se déclenche lorsqu’une exécution du flux du services d’identités démarre le traitement des données. En d’autres termes, les données ingérées sont chargées du lac de données vers le service d’identités. |
| Informations relatives à l’ingestion d’identités | Succès de l’exécution du flux du service d’identités | Cette alerte se déclenche lorsque les données sont correctement chargées du lac de données vers le service d’identités. |
| Retards, échecs et erreurs de l’ingestion d’identités | Retard d’exécution du flux du service d’identités | Cette alerte se déclenche lorsqu’une exécution du flux du service d’identités dure plus de 150 minutes. |
| Retards, échecs et erreurs de l’ingestion d’identités | Échec de l’exécution du flux du service d’identités | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données dans le service d’identités. |

{style=&quot;table-layout:auto&quot;}

## Profil client en temps réel

Les règles d’alerte suivantes sont spécifiques au [profil client en temps réel](../../profile/home.md) :

| Abonnement aux événements I/O | Règle d’alerte | Description |
| --- | --- | --- |
| Informations concernant l’ingestion de profils | Début de l’exécution du flux de profils | Cette alerte se déclenche lorsqu’une exécution du flux de profils démarre le traitement des données. |
| Informations concernant l’ingestion de profils | Succès de l’exécution du flux de profils | Cette alerte se déclenche lorsque les données sont chargées correctement dans le profil à partir du lac de données. |
| Retards, échecs et erreurs de l’ingestion de profils | Retard d’exécution du flux de profils | Cette alerte se déclenche lorsque le chargement des données du lac de données dans le profil dure plus de 150 minutes. |
| Retards, échecs et erreurs de l’ingestion de profils | Échec de l’exécution du flux de profils | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données dans le profil. |

{style=&quot;table-layout:auto&quot;}

## Segmentation

Les règles d’alerte suivantes sont spécifiques à [Segmentation Service](../../segmentation/home.md) :

| Abonnement aux événements I/O | Règle d’alerte | Description |
| --- | --- | --- |
| Informations relatives à la tâche d’évaluation de segments | Début de la tâche relative aux segments | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segments commence à traiter des données. |
| Informations relatives à la tâche d’évaluation de segments | Réussite de la tâche relative aux segments | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segments se termine avec succès. |
| Retards, échecs et erreurs relatifs à la tâche d’évaluation de segments | Retard de la tâche relative aux segments | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segments dure plus de 150 minutes. |
| Retards, échecs et erreurs relatifs à la tâche d’évaluation de segments | Échec de la tâche relative aux segments | Cette alerte se déclenche lorsqu’une tâche d’évaluation de segments génère une erreur. |
| Retards, échecs et erreurs relatifs à la tâche d’évaluation de segments | Définition de segments désactivée | Cette alerte se déclenche lorsqu’une définition de segments est désactivée en raison d’une erreur interne. Cette action déclenche automatiquement un dispositif d’urgence pour qu’une équipe d’ingénieurs Adobe enquête sur le problème. Cette alerte a pour seul but d’être informative et ne nécessite aucune action de votre part. |

{style=&quot;table-layout:auto&quot;}

## Destinations

Les règles d’alerte suivantes sont spécifiques aux [destinations](../../destinations/home.md) :

| Abonnement aux événements I/O | Règle d’alerte | Description |
| --- | --- | --- |
| Informations relatives à l’exécution du flux de destinations | Début de l’exécution du flux de destinations | Cette alerte se déclenche lorsqu’une exécution de flux de destinations commence à activer un segment. |
| Informations relatives à l’exécution du flux de destinations | Succès de l’exécution du flux de destinations | Cette alerte se déclenche lorsqu’un segment est activé avec succès vers une destination. |
| Délais, échecs et erreurs de l’exécution du flux de destinations | Retard de l’exécution du flux de destinations | Cette alerte se déclenche lorsqu’une exécution de flux de destinations dure plus de 150 minutes pour activer un segment. |
| Délais, échecs et erreurs de l’exécution du flux de destinations | Échec de l’exécution du flux de destinations | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’activation d’un segment vers une destination. |

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
