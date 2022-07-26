---
title: Classe de prière
description: Ce document présente la classe de lecteur dans le modèle de données d’expérience (XDM).
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
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
