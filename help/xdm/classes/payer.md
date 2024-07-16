---
title: Classe de prière
description: Découvrez la classe Payer dans le modèle de données d’expérience (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# [!UICONTROL Classe Payer]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Payer] capture l’ensemble minimum de propriétés qui définissent une entité commerciale payante qui collecte des données relatives aux compagnies d’assurance (telles que l’assurance maladie).

![Structure de classe](../images/classes/payer.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Comme ce champ est généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `payerId` | [!UICONTROL Chaîne] | Identifiant unique du lecteur. |
| `payerName` | [!UICONTROL Chaîne] | Nom du payeur. |

{style="table-layout:auto"}
