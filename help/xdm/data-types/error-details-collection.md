---
title: Type de données de collection Détails de l’erreur
description: Découvrez le type de données XDM (Error Details Collection Experience Data Model).
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL Détails de l’erreur] Type de données de collection

[!UICONTROL Error Details] La collection est un type de données XDM (Experience Data Model) standard qui décrit les détails de l’erreur. Utilisez le type de données Collection [!UICONTROL Détails de l’erreur] pour capturer les détails de la source de l’erreur et de l’identification. L’ID d’erreur identifie l’erreur et la source de l’erreur indique si elle provient du lecteur ou d’une source externe.

![Schéma du type de données Error Details Information.](../images/data-types/error-details-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID d’erreur] | `name` | Chaîne | Non | ID de l’erreur. |
| [!UICONTROL Error Source] | `source` | Chaîne | Non | Source de l’erreur. Énuméré : &quot;joueur&quot;, &quot;externe&quot; avec leurs significations respectives. |

{style="table-layout:auto"}
