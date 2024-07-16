---
title: Type de données de rapport Détails sur les métadonnées personnalisées
description: Découvrez le type de données XDM (Modèle de données d’expérience de création de rapports sur les métadonnées personnalisées).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 10%

---

# [!UICONTROL Détails sur les métadonnées personnalisées] Type de données de rapport

[!UICONTROL Détails des métadonnées personnalisées] La création de rapports est un type de données XDM (Experience Data Model) standard qui définit une structure pour le stockage de métadonnées personnalisées. Le type de données de rapport [!UICONTROL Détails des métadonnées personnalisées] capture des détails tels que le nom et la valeur des métadonnées personnalisées associées au contenu ou aux interactions. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs de collecte multimédia envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports.

![ Diagramme du type de données Rapports de détails de métadonnées personnalisés.](../images/data-types/the-custom-metadata-reporting.png)

| Nom d’affichage | Propriété | Type de données | Description |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nom du champ de métadonnées personnalisé] | `name` | Chaîne | Nom du champ personnalisé. |
| [!UICONTROL Valeur du champ de métadonnées personnalisé] | `value` | Chaîne | La valeur du champ personnalisé. |

{style="table-layout:auto"}
