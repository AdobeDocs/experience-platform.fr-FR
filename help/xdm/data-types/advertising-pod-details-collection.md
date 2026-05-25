---
title: Type De Données De Collection De Détails De Capsule Advertising
description: Découvrez le type de données XDM (Modèle de données d’expérience) de la collecte de détails de capsule Advertising.
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
TQID: https://experienceleague.adobe.com/nxaug84PrV0OKnqEeBlms4aJNmOkOeuLsQjofl-PQv4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 9%

---

# Type de données de la collecte de [!UICONTROL Advertising Pod Details]

La collecte de [!UICONTROL Advertising Pod Details] est un type de données standard du modèle de données d’expérience (XDM). Il définit une séquence ou un groupe d’annonces généralement lues successivement pendant les pauses de contenu. Utilisez le type de données [!UICONTROL Advertising Pod Details] la collecte de données pour capturer des détails tels que l’identifiant de la coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités dans la coupure et le décalage de la coupure publicitaire dans la chronologie du contenu en secondes.

![Diagramme du type de données Collecte d’informations sur les détails de capsule Advertising.](../images/data-types/advertising-pod-details-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-----------------------------------------|-----------------|-----------|----------|---------------------------------------------------------|
| [!UICONTROL Ad In Pod Position] | `index` | Entier | Oui | Index de la publicité à l’intérieur du début de la coupure publicitaire parent. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | Non | Nom facilement compréhensible de la coupure publicitaire. |
| [!UICONTROL Pod Offset] | `offset` | Entier | Oui | Décalage de la coupure publicitaire dans le contenu, en secondes. |

{style="table-layout:auto"}
