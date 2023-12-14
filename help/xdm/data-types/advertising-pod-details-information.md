---
title: Type de données d’informations sur les détails de la capsule publicitaire
description: Découvrez le type de données du modèle de données d’expérience (XDM) Advertising Pod Details.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# [!UICONTROL Informations sur les détails de la capsule publicitaire] type de données

[!UICONTROL Informations sur les détails de la capsule publicitaire] est un type de données XDM (Experience Data Model) standard. Il définit une séquence ou un groupe de publicités généralement lues l’une après l’autre lors des pauses de contenu. Utilisez la variable [!UICONTROL Informations sur les détails de la capsule publicitaire] type de données pour capturer des détails tels que l’identifiant de coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités pendant la coupure et le décalage de la coupure publicitaire dans la chronologie du contenu en secondes.

![Schéma du type de données Informations sur les détails de la capsule publicitaire.](../images/data-types/advertising-pod-details-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID de coupure publicitaire] | `ID` | chaîne | Identifiant de la coupure publicitaire. |
| [!UICONTROL Nom convivial de la capsule] | `friendlyName` | chaîne | Nom facile à comprendre de la coupure publicitaire. |
| [!UICONTROL Position de la publicité dans la capsule] | `index` | nombre entier | Index de la publicité dans le démarrage de la coupure publicitaire parent. |
| [!UICONTROL Décalage de capsule] | `offset` | nombre entier | **Obligatoire** Décalage de la coupure publicitaire dans le contenu, en secondes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
