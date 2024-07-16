---
title: Notes de mise à jour de l’extension Adobe Experience Platform Cloud Connector
description: Notes de mise à jour les plus récentes pour l’extension Cloud Connector dans Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 35%

---

# Notes de mise à jour de l’extension Adobe Experience Platform Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 17 janvier 2023

v1.0.1

* Correction d’un problème en raison duquel un fichier JSON valide collé dans la zone de texte Corps brut était enregistré sous la forme d’une chaîne au lieu d’un fichier JSON.
* Ne pas autoriser la définition du corps sur des requêtes GET ou HEAD.
* Correction d’un bogue en raison duquel l’enregistrement d’une réponse supérieure à 5 Ko faisait échouer l’exécution de la règle.
