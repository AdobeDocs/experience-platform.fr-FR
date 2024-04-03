---
title: Type de données de collection Détails de métadonnées personnalisés
description: Découvrez le type de données XDM (Custom Metadata Details) Collection Experience Data Model (XDM).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 15%

---

# [!UICONTROL Détails des métadonnées personnalisées] Type de données de collecte

[!UICONTROL Détails des métadonnées personnalisées] Collection est un type de données XDM (Experience Data Model) standard qui définit une structure pour le stockage de métadonnées personnalisées. Utilisez la variable [!UICONTROL Détails des métadonnées personnalisées] Type de données de collection pour capturer des détails tels que le nom et la valeur des métadonnées personnalisées associées au contenu ou aux interactions.

![Schéma du type de données Collection de détails de métadonnées personnalisées.](../images/data-types/the-custom-metadata-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------------------|------------------|-----------|----------|-------------------------------|
| [!UICONTROL Nom du champ de métadonnées personnalisé] | `name` | Chaîne | Non | Nom du champ personnalisé. |
| [!UICONTROL Valeur du champ de métadonnées personnalisé] | `value` | Chaîne | Non | La valeur du champ personnalisé. |

{style="table-layout:auto"}
