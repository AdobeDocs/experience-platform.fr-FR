---
title: Liste des types de données de collection finale des états
description: Découvrez le type de données XDM (Experience Data Model) List of States End Collection Data Type (Liste des états).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL Fin de la liste des états] type de données

Le type de données Liste des états Collection de fin est un type de données XDM (Experience Data Model) conçu pour représenter des informations relatives à l’état final de divers attributs du lecteur. Il comprend la variable [!UICONTROL Nom de l’état du lecteur] qui indique l’état d’attribut spécifique (par exemple, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Ce type de données est utilisé pour capturer et décrire les conditions initiales des différents états du lecteur.

![Diagramme de type de données Liste des états de collecte de fin .](../images/data-types/list-of-states-end-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nom de l’état du lecteur] | `name` | Chaîne | Non | Nom de l’état du lecteur. Énuméré : &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; avec leurs significations respectives. |

{style="table-layout:auto"}
