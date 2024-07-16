---
title: Liste des états Début de la collecte Type de données
description: Découvrez le type de données XDM (Experience Data Model) List of States Start Data Type (Liste des états).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# Type de données [!UICONTROL Liste des états démarrés]

Le type de données [!UICONTROL List of States Start] est un type de données XDM (Experience Data Model) conçu pour représenter des informations relatives à l’état de départ de divers attributs de lecteur. Elle comprend les propriétés [!UICONTROL Player State Name] qui indiquent l’état d’attribut spécifique (par exemple, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Ce type de données est utilisé pour capturer et décrire les conditions initiales des différents états du lecteur.

![ Diagramme de type de données [!UICONTROL List of States Start].](../images/data-types/list-of-states-start-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nom de l’état du lecteur] | `name` | Chaîne | Non | Nom de l’état du lecteur. Énuméré : &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; avec leurs significations respectives. |

{style="table-layout:auto"}
