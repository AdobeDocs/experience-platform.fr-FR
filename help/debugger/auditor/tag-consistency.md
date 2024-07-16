---
title: Référence du test de cohérence des balises
description: Découvrez comment l’Auditor teste la cohérence des balises dans Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 40%

---

# Référence du test de cohérence des balises

Cette référence fournit des informations supplémentaires sur la manière dont la fonction d’audit dans les tests d’Adobe Experience Platform Debugger pour assurer la cohérence des balises.

>[!NOTE]
>
>Pour plus d’informations sur les tests d’Auditor dans Platform Debugger, consultez la [présentation des fonctionnalités d’Auditor](./overview.md).

Les tests de cohérence des balises recherchent les incohérences entre toutes les pages numérisées. Il s’agit de valeurs ou de configurations qui doivent être identiques sur toutes les pages du site pour garantir une collecte de données précise.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Adobe Analytics - Version de code cohérente | 5 | Plusieurs versions du code Analytics ont été trouvées. | Remplacez toutes les instances d’Analytics par la version actuelle.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr) |

{style="table-layout:auto"}
