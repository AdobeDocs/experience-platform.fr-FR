---
title: Type de données de collection des détails des métadonnées personnalisées
description: Découvrez le type de données Modèle de données d’expérience (XDM) de la collecte de détails de métadonnées personnalisées.
exl-id: e2fa65ea-b738-43c6-90f1-1968dd83b963
TQID: https://experienceleague.adobe.com/hYfRmp81jY1jrSqnXT9yEh-bXRHl6ordf3HtU25emuM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 18%

---

# Type de données de la collecte de [!UICONTROL Custom Metadata Details]

La collecte de [!UICONTROL Custom Metadata Details] est un type de données standard du modèle de données d’expérience (XDM) qui définit une structure de stockage des métadonnées personnalisées. Utilisez le type de données Collection de [!UICONTROL Custom Metadata Details] pour capturer des informations telles que le nom et la valeur de métadonnées personnalisées associées au contenu ou aux interactions.

![Diagramme du type de données Collection de détails de métadonnées personnalisées.](../images/data-types/the-custom-metadata-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------------------|------------------|-----------|----------|-------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | Non | Nom du champ personnalisé. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | Non | Valeur du champ personnalisé. |

{style="table-layout:auto"}
