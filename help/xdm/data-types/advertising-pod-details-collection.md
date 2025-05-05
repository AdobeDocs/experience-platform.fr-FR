---
title: Type de données de collecte Détails de la capsule Advertising
description: Découvrez le type de données XDM (Modèle de données d’expérience de collecte de détails de la capsule Advertising).
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Détails de la capsule Advertising] Type de données de collection

[!UICONTROL &#x200B; La collection &lbrace;Advertising Pod Details] est un type de données XDM (Experience Data Model) standard. Il définit une séquence ou un groupe de publicités généralement lues l’une après l’autre lors des pauses de contenu. Utilisez le type de données Collection [!UICONTROL Détails de la capsule Advertising] pour capturer des détails tels que l’ID de coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités pendant la coupure et le décalage de la coupure publicitaire dans la chronologie du contenu en secondes.

![Schéma du type de données Collecte d’informations sur la capsule Advertising.](../images/data-types/advertising-pod-details-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-----------------------------------------|-----------------|-----------|----------|---------------------------------------------------------|
| [!UICONTROL Position de la publicité dans la capsule] | `index` | Entier | Oui | Index de la publicité dans le démarrage de la coupure publicitaire parent. |
| [!UICONTROL Nom convivial de la capsule] | `friendlyName` | Chaîne | Non | Nom facile à comprendre de la coupure publicitaire. |
| [!UICONTROL Décalage de capsule] | `offset` | Entier | Oui | Décalage de la coupure publicitaire dans le contenu, en secondes. |

{style="table-layout:auto"}
