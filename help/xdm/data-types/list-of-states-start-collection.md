---
title: Type de données de collecte de début de la liste des états
description: Découvrez le type de données Modèle de données d’expérience (XDM) de type Liste d’états démarrés .
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 8%

---

# Type de données [!UICONTROL List of States Start]

Le type de données [!UICONTROL List of States Start] est un type de données de modèle de données d’expérience (XDM) conçu pour représenter les informations liées à l’état de départ de divers attributs du lecteur. Elle inclut les propriétés [!UICONTROL Player State Name] qui indiquent l’état spécifique de l’attribut (par exemple, « fullscreen », « mute », « closedCaptioning »). Ce type de données est utilisé pour capturer et décrire les conditions initiales de différents états du lecteur.

![Diagramme de [!UICONTROL List of States Start] type de données.](../images/data-types/list-of-states-start-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | chaîne | Non | Nom de l’état du lecteur. Énumérées : « fullscreen », « mute », « closeCaptioning », « pictureInPicture », « inFocus » avec leurs significations respectives. |

{style="table-layout:auto"}
