---
title: Type de données de collecte de fin de liste d’états
description: Découvrez le type de données Modèle de données d’expérience (XDM) du type de données de collecte d’états de la liste.
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
TQID: https://experienceleague.adobe.com/aRF5lJ7YEzL66F0EE8rGCv94hydwmB1LDARvbyG27Rc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 121
ht-degree: 7%

---

# Type de données [!UICONTROL List of States End]

Le type de données de collecte de fin de liste d’états est un type de données de modèle de données d’expérience (XDM) conçu pour représenter les informations relatives à l’état de fin de divers attributs du lecteur. Elle inclut les propriétés [!UICONTROL Player State Name] qui indiquent l’état spécifique de l’attribut (par exemple, « fullscreen », « mute », « closedCaptioning »). Ce type de données est utilisé pour capturer et décrire les conditions initiales de différents états du lecteur.

![Diagramme du type de données de collecte de fin de liste d’états.](../images/data-types/list-of-states-end-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Non | Nom de l’état du lecteur. Énumérées : « fullscreen », « mute », « closeCaptioning », « pictureInPicture », « inFocus » avec leurs significations respectives. |

{style="table-layout:auto"}
