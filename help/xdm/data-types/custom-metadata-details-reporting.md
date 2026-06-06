---
title: Type de données de rapport des détails des métadonnées personnalisées
description: Découvrez le type de données Modèle de données d’expérience de création de rapports (XDM) des détails de métadonnées personnalisées.
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
TQID: https://experienceleague.adobe.com/tev17tpO-WDik-ZUh4MgAnBXaHNbZYz4bWU2wXl7J6k
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 8%

---

# Type de données [!UICONTROL Custom Metadata Details] Reporting

[!UICONTROL Custom Metadata Details] Reporting est un type de données standard des modèles de données d’expérience (XDM) qui définit une structure de stockage des métadonnées personnalisées. Le type de données Rapports [!UICONTROL Custom Metadata Details] capture des détails tels que le nom et la valeur des métadonnées personnalisées associées au contenu ou aux interactions.

+++Sélectionnez cette option pour afficher un diagramme du type de données [!UICONTROL Custom Metadata Details] Reporting .
![Diagramme du type de données Rapports sur les détails des métadonnées personnalisées.](../images/data-types/the-custom-metadata-reporting.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaReporting` : champs calculés par le serveur principal des médias en flux continu à partir des données `mediaCollection` envoyées par votre implémentation. Il s’agit des champs qu’Adobe ingère dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

| Nom d’affichage | Propriété | Type de données | Description |
|---|---|---|---|
| [!UICONTROL Custom Metadata Field Name] | `name` | chaîne | Nom du champ personnalisé. |
| [!UICONTROL Custom Metadata Field Value] | `value` | chaîne | Valeur du champ personnalisé. |

Voir [custommetadatadetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.
