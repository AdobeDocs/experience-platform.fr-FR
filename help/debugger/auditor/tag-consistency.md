---
title: Référence du test de cohérence des balises
description: Découvrez comment l’auditeur teste la cohérence des balises dans Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
TQID: https://experienceleague.adobe.com/W33I7lTeT8ywcsCdOnKaa9PJurbWt811P5T1Pc7KjOc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 124
ht-degree: 42%

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
