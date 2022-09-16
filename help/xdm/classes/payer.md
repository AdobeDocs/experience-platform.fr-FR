---
title: Classe de prière
description: Ce document présente la classe de lecteur dans le modèle de données d’expérience (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 7%

---

# [!UICONTROL Payer] class

Dans le modèle de données d’expérience (XDM), la variable [!UICONTROL Payer] capture l’ensemble minimal de propriétés qui définissent une entité commerciale payante qui collecte des données relatives aux compagnies d’assurance (telles que l’assurance maladie).

![Structure de classe](../images/classes/payer.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `payerId` | [!UICONTROL Chaîne] | Identifiant unique du lecteur. |
| `payerName` | [!UICONTROL Chaîne] | Nom du payeur. |

{style=&quot;table-layout:auto&quot;}
