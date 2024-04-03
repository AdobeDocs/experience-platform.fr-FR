---
title: Type de données de collection Détails de l’erreur
description: Découvrez le type de données XDM (Error Details Collection Experience Data Model).
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 9%

---

# [!UICONTROL Détails de l’erreur] Type de données de collecte

[!UICONTROL Détails de l’erreur] Collection est un type de données XDM (Experience Data Model) standard qui décrit les détails d’erreur. Utilisez la variable [!UICONTROL Détails de l’erreur] Type de données de collecte pour capturer les détails de la source de l’erreur et de l’identification. L’ID d’erreur identifie l’erreur et la source de l’erreur indique si elle provient du lecteur ou d’une source externe.

![Schéma du type de données Error Details Information .](../images/data-types/error-details-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Identifiant d’erreur] | `name` | Chaîne | Non | ID d’erreur. |
| [!UICONTROL Source de l’erreur] | `source` | Chaîne | Non | Source de l’erreur. Énuméré : &quot;joueur&quot;, &quot;externe&quot; avec leurs significations respectives. |

{style="table-layout:auto"}
