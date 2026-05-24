---
title: Classe de plan
description: Découvrez la classe Plan dans le modèle de données d’expérience (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
TQID: https://experienceleague.adobe.com/RI-7KFR-Q5V6-iuAt9oO70TXSFFOvOSjBPBH0fTMNn8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 139
ht-degree: 3%

---

# Classe [!UICONTROL Plan]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Plan] capture l’ensemble minimal de propriétés qui définissent un plan, comme un plan de santé ou un plan d’assurance.

![Structure de classe](../images/classes/plan.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de déterminer l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’ID uniques si vous le souhaitez. |
| `planId` | [!UICONTROL String] | Identifiant unique du plan. |
| `planName` | [!UICONTROL String] | Nom du plan. |

{style="table-layout:auto"}

La classe peut être étendue avec le groupe de champs [&#128279;](../field-groups/plan/healthcare-plan-details.md) pour décrire plus de détails sur un régime d’assurance maladie.[!UICONTROL Healthcare Plan Details]
