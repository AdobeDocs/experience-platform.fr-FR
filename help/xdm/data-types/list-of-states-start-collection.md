---
title: Liste des états Début de la collecte Type de données
description: Découvrez le type de données XDM (Experience Data Model) List of States Start Data Type (Liste des états).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Liste des états - Début] type de données

La variable [!UICONTROL Liste des états - Début] Le type de données est un type de données de modèle de données d’expérience (XDM) conçu pour représenter des informations relatives à l’état de départ de divers attributs de lecteur. Il comprend la variable [!UICONTROL Nom de l’état du lecteur] qui indique l’état d’attribut spécifique (par exemple, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Ce type de données est utilisé pour capturer et décrire les conditions initiales des différents états du lecteur.

![Un diagramme de [!UICONTROL Liste des états - Début] type de données.](../images/data-types/list-of-states-start-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nom de l’état du lecteur] | `name` | Chaîne | Non | Nom de l’état du lecteur. Énuméré : &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; avec leurs significations respectives. |

{style="table-layout:auto"}
