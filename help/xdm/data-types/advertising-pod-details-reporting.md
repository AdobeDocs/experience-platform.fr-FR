---
title: Type de données de rapport Détails de la capsule Advertising
description: Découvrez le type de données XDM (Advertising Pod Details Reporting Experience Data Model).
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# [!UICONTROL Rapports sur les détails de la capsule publicitaire] type de données

[!UICONTROL Rapports sur les détails de la capsule publicitaire] est un type de données XDM (Experience Data Model) standard. Il définit une séquence ou un groupe de publicités généralement lues l’une après l’autre lors des pauses de contenu. Utilisez la variable [!UICONTROL Rapports sur les détails de la capsule publicitaire] type de données pour capturer des détails tels que l’identifiant de coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités pendant la coupure et le décalage de la coupure publicitaire dans la chronologie du contenu en secondes.

![Diagramme du type de données Rapports sur les détails de la capsule publicitaire.](../images/data-types/advertising-pod-details-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID de coupure publicitaire] | `ID` | Chaîne | Identifiant de la coupure publicitaire. |
| [!UICONTROL Nom convivial de la capsule] | `friendlyName` | Chaîne | Nom facile à comprendre de la coupure publicitaire. |
| [!UICONTROL Position de la publicité dans la capsule] | `index` | Entier | Index de la publicité dans le démarrage de la coupure publicitaire parent. |
| [!UICONTROL Décalage de capsule] | `offset` | Entier | **Obligatoire** Décalage de la coupure publicitaire dans le contenu, en secondes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
