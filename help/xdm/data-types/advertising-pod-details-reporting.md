---
title: Type de données de rapport Détails de la capsule Advertising
description: Découvrez le type de données XDM (Modèle de données d’expérience de création de rapports sur les détails de la capsule Advertising).
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# [!UICONTROL Rapport sur les détails de la capsule Advertising] type de données

[!UICONTROL &#x200B; La création de rapports sur les détails de la capsule Advertising &#x200B;] est un type de données XDM (Experience Data Model) standard. Il définit une séquence ou un groupe de publicités généralement lues l’une après l’autre lors des pauses de contenu. Utilisez le type de données [!UICONTROL Rapport sur les détails de la capsule Advertising] pour capturer des détails tels que l’ID de coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités pendant la coupure et le décalage de la coupure publicitaire dans la chronologie du contenu en secondes.

![&#x200B; Diagramme du type de données de rapport Détails de la capsule Advertising.](../images/data-types/advertising-pod-details-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID de coupure publicitaire] | `ID` | Chaîne | Identifiant de la coupure publicitaire. |
| [!UICONTROL Nom convivial de la capsule] | `friendlyName` | Chaîne | Nom facile à comprendre de la coupure publicitaire. |
| [!UICONTROL Position de la publicité dans la capsule] | `index` | Entier | Index de la publicité dans le démarrage de la coupure publicitaire parent. |
| [!UICONTROL Décalage de capsule] | `offset` | Entier | **Obligatoire** Décalage de la coupure publicitaire dans le contenu, en secondes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
