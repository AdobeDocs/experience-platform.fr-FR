---
title: Type de données de collection Détails de la capsule Advertising
description: Découvrez le type de données XDM (Advertising Pod Details Collection Experience Data Model).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Détails de la capsule publicitaire] Type de données de collecte

[!UICONTROL Détails de la capsule publicitaire] La collecte est un type de données XDM (Experience Data Model) standard. Il définit une séquence ou un groupe de publicités généralement lues l’une après l’autre lors des pauses de contenu. Utilisez la variable [!UICONTROL Détails de la capsule publicitaire] Type de données de collection pour la capture de détails tels que l’ID de coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités pendant la coupure et le décalage de la coupure publicitaire dans la chronologie du contenu en secondes.

![Schéma du type de données Collection d’informations sur la capsule Advertising.](../images/data-types/advertising-pod-details-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Position de la publicité dans la capsule] | `index` | Entier | Oui | Index de la publicité dans le démarrage de la coupure publicitaire parent. |
| [!UICONTROL Nom convivial de la capsule] | `friendlyName` | Chaîne | Non | Nom facile à comprendre de la coupure publicitaire. |
| [!UICONTROL Décalage de capsule] | `offset` | Entier | Oui | Décalage de la coupure publicitaire dans le contenu, en secondes. |
