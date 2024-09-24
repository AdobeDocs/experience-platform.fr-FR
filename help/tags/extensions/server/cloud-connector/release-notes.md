---
title: Notes de mise à jour de l’extension Connecteur cloud dans Adobe Experience Platform
description: Notes de mise à jour les plus récentes de l’extension Connecteur cloud dans Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Notes de mise à jour de l’extension Connecteur cloud dans Adobe Experience Platform

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 17 janvier 2023

v1.0.1

* Correction d’un problème en raison duquel du code JSON valide collé dans la zone de texte de corps brut était enregistré sous la forme d’une chaîne au lieu de code JSON.
* Pas d’autorisation de définition du corps sur des requêtes GET ou HEAD.
* Correction d’un bug en raison duquel l’enregistrement d’une réponse supérieure à 5 Ko faisait échouer l’exécution de la règle.
