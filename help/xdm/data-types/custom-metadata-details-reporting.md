---
title: Type de données de rapport Détails sur les métadonnées personnalisées
description: Découvrez le type de données XDM (Modèle de données d’expérience de création de rapports sur les métadonnées personnalisées).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 10%

---

# [!UICONTROL Détails des métadonnées personnalisées] Type de données de reporting

[!UICONTROL Détails des métadonnées personnalisées] La création de rapports est un type de données XDM (Experience Data Model) standard qui définit une structure pour le stockage de métadonnées personnalisées. La variable [!UICONTROL Détails des métadonnées personnalisées] Le type de données des rapports capture des détails tels que le nom et la valeur des métadonnées personnalisées associées au contenu ou aux interactions. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs de collecte multimédia envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports.

![Diagramme du type de données Rapports sur les détails des métadonnées personnalisées.](../images/data-types/the-custom-metadata-reporting.png)

| Nom d’affichage | Propriété | Type de données | Description |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nom du champ de métadonnées personnalisé] | `name` | Chaîne | Nom du champ personnalisé. |
| [!UICONTROL Valeur du champ de métadonnées personnalisé] | `value` | Chaîne | La valeur du champ personnalisé. |

{style="table-layout:auto"}
