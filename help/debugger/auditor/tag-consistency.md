---
title: Référence du test de cohérence des balises
description: Découvrez comment l’auditeur teste la cohérence des balises dans Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 40%

---

# Référence du test de cohérence des balises

Cette référence fournit des informations supplémentaires sur la manière dont l’auditeur d’Adobe Experience Platform Debugger teste la cohérence des balises.

>[!NOTE]
>
>Pour plus d’informations sur les tests de l’auditeur dans Experience Platform Debugger, consultez la [présentation des fonctionnalités de l’auditeur](./overview.md).

Les tests de cohérence des balises recherchent les incohérences sur toutes les pages numérisées. Il s’agit de valeurs ou de configurations qui doivent être identiques sur toutes les pages du site pour garantir une collecte de données précise.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Adobe Analytics - Version de code cohérente | 5 | Plusieurs versions du code Analytics ont été trouvées. | Remplacez toutes les instances d’Analytics par la version actuelle.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr) |

{style="table-layout:auto"}
