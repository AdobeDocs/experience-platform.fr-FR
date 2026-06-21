---
title: Classe De Médicaments
description: Découvrez la classe Médicaments dans le modèle de données d’expérience (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
TQID: https://experienceleague.adobe.com/y2hLHq-H5on3MVCADj4Yj9A5Qd29LJ6zwXQx2AMuNy8
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 147
ht-degree: 4%

---

# Classe [!UICONTROL Médicaments]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Médicament] capture l’ensemble minimum des propriétés qui définissent une substance utilisée pour un traitement médical, en particulier un médicament ou un médicament.

![Structure de classe](../images/classes/medication.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de déterminer l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’ID uniques si vous le souhaitez. |
| `medicationId` | [!UICONTROL Chaîne] | Identifiant unique du médicament. |
| `medicationName` | [!UICONTROL Chaîne] | Le nom du médicament. |

{style="table-layout:auto"}

La classe peut être étendue avec le groupe de champs [[!UICONTROL Médicaments pour les soins de santé] ](../field-groups/medication/healthcare-medication.md) pour décrire plus de détails sur le médicament ou le médicament.
