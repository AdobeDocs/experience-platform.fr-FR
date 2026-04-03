---
title: Type de données de collecte de fin de liste d’états
description: Découvrez le type de données Modèle de données d’expérience (XDM) du type de données de collecte d’états de la liste.
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# Type de données [!UICONTROL List of States End]

Le type de données de collecte de fin de liste d’états est un type de données de modèle de données d’expérience (XDM) conçu pour représenter les informations relatives à l’état de fin de divers attributs du lecteur. Elle inclut les propriétés [!UICONTROL Player State Name] qui indiquent l’état spécifique de l’attribut (par exemple, « fullscreen », « mute », « closedCaptioning »). Ce type de données est utilisé pour capturer et décrire les conditions initiales de différents états du lecteur.

![Diagramme du type de données de collecte de fin de liste d’états.](../images/data-types/list-of-states-end-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | chaîne | Non | Nom de l’état du lecteur. Énumérées : « fullscreen », « mute », « closeCaptioning », « pictureInPicture », « inFocus » avec leurs significations respectives. |

{style="table-layout:auto"}
