---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Règles d’alerte standard
description: 'Ce document couvre les règles d’alerte prédéfinies fournies par Experience Platform. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 16%

---


# Règles d’alerte standard

Adobe Experience Platform fournit plusieurs règles d’alerte prédéfinies que vous pouvez activer pour votre organisation. Le tableau ci-dessous présente les détails de ces règles d’alerte fournies par l’Adobe. Pour plus d’informations sur les alertes en Experience Platform, consultez la [présentation des alertes](./overview.md).

| Composants de  | Description | Fréquence d&#39;évaluation | Fenêtre de répétition |
| --- | --- | --- | --- |
| Seuil de droits dépassé | Cette alerte se déclenche lorsque le nombre de profils créés dépasse 80 % des droits de votre entreprise. | 30 secondes | N/A |
| Aucune activité d’ingestion au cours des dernières 24 heures | Cette alerte se déclenche lorsqu’aucune nouvelle donnée n’a été ingérée au cours des dernières 24 heures. | 1 jour | 1 jour |
| La source SFTP n’a pas de données ingérées | Cette alerte se déclenche lorsqu’une [source SFTP](../../sources/connectors/cloud-storage/sftp.md) n’a ingéré aucune donnée au cours d’une période donnée. | 1 jour | 1 jour |
| Le taux d&#39;erreur d&#39;ingestion a dépassé | Cette alerte se déclenche lorsque le taux d’erreur d’ingestion des données dépasse 20 %. | 30 secondes | 30 secondes |
| Message du flux | Cette alerte lorsqu’un message de flux de partage d’identité a été envoyé à un utilisateur à l’aide de [Correspondance de segment](../../segmentation/ui/segment-match.md). | S.O. | S.O. |
| Accès au flux révoqué | Cette alerte se déclenche lorsqu’un autre utilisateur de Platform révoque l’accès à un flux de partage d’identité à l’aide de [Correspondance de segment](../../segmentation/ui/segment-match.md). | S.O. | S.O. |
| Flux modifié | Cette alerte se déclenche lorsqu’un flux de partage d’identité est modifié par un utilisateur à l’aide de [Correspondance de segment](../../segmentation/ui/segment-match.md). | S.O. | S.O. |
| Flux partagé | Cette alerte se déclenche lorsqu’un utilisateur partage un nouveau flux dans [Correspondance de segment](../../segmentation/ui/segment-match.md). | S.O. | S.O. |
| Requête de lien | Cette alerte se déclenche lorsqu’un utilisateur demande à se connecter pour le partage de partenaire. | S.O. | S.O. |
| Action de lien | Cette alerte se déclenche lorsqu’un utilisateur accepte une demande de connexion pour le partage avec les partenaires. | S.O. | S.O. |
| Définition de segment désactivée | Cette alerte se déclenche lorsqu’une définition de segment est désactivée. | S.O. | S.O. |
| Délai de tâche de segment | Cette alerte se déclenche lorsqu’une tâche de segmentation prend plus de 150 minutes. | 30 secondes | 3 heures |
| Échec de l’exécution du flux des sources | Cette alerte se déclenche lorsqu’une erreur se produit lors de l’ingestion de données à partir d’une connexion source. | S.O. | S.O. |
| Succès de l’exécution du flux de sources | Cette alerte se déclenche lorsque les données sont correctement ingérées à partir d’une connexion source. | S.O. | S.O. |

{style=&quot;table-layout:auto&quot;}