---
title: Type de données des détails d’implémentation
description: Découvrez le type de données Modèle de données d’expérience (XDM) des détails d’implémentation.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
TQID: https://experienceleague.adobe.com/Z3qrTLOz6olUq4Ei1Xcw0TJpAs5P5PN5P-kAycerbyE
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 123
ht-degree: 14%

---

# [!UICONTROL Détails d’implémentation] type de données

[!UICONTROL &#x200B; Détails d’implémentation &#x200B;] est un type de données standard du modèle de données d’expérience (XDM) qui décrit une implémentation technologique, telle qu’une API ou un SDK.

![Structure du type de données](../images/data-types/implementation-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `environment` | Chaîne | Environnement de la mise en œuvre. |
| `name` | Chaîne | Identifiant du SDK ou du point d’entrée. Tous les SDK ou points d’entrée sont identifiés via un URI, y compris les extensions. |
| `version` | Chaîne | Version de l’API ou du SDK. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
