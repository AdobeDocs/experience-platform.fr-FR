---
title: Classe de payeur
description: Découvrez la classe Payeur dans le modèle de données d’expérience (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
TQID: https://experienceleague.adobe.com/4ltQCVMSsInFFLCH6GcxTLEpFUvGIHHM-NT30z12JY0
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 126
ht-degree: 3%

---

# Classe [!UICONTROL Payer]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Payer] capture l’ensemble minimal de propriétés qui définissent une entité professionnelle du payeur qui collecte des données relatives aux compagnies d’assurance (telles que l’assurance maladie).

![Structure de classe](../images/classes/payer.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de déterminer l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’ID uniques si vous le souhaitez. |
| `payerId` | [!UICONTROL String] | Identifiant unique du payeur. |
| `payerName` | [!UICONTROL String] | Nom du payeur. |

{style="table-layout:auto"}
