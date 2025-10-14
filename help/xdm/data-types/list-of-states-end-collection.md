---
title: Liste des types de données de collection finale des états
description: Découvrez le type de données XDM (Experience Data Model) List of States End Collection Data Type (Liste des états).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# Type de données [!UICONTROL Liste des états terminés]

Le type de données Liste des états Collection de fin est un type de données XDM (Experience Data Model) conçu pour représenter des informations relatives à l’état final de divers attributs du lecteur. Elle comprend les propriétés [!UICONTROL Player State Name] qui indiquent l’état d’attribut spécifique (par exemple, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Ce type de données est utilisé pour capturer et décrire les conditions initiales des différents états du lecteur.

![&#x200B; Diagramme de type de données Liste des états de collecte de fin.](../images/data-types/list-of-states-end-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nom de l’état du lecteur] | `name` | Chaîne | Non | Nom de l’état du lecteur. Énuméré : &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; avec leurs significations respectives. |

{style="table-layout:auto"}
