---
title: Type de données de collecte de début de la liste des états
description: Découvrez le type de données Modèle de données d’expérience (XDM) de type Liste d’états démarrés .
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
TQID: https://experienceleague.adobe.com/fr4TJgxCJYOVSKHbWpyGDsmupivHPCCyDY7UXaxRU3Y
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 108
ht-degree: 8%

---

# Type de données [!UICONTROL List of States Start]

Le type de données [!UICONTROL List of States Start] est un type de données de modèle de données d’expérience (XDM) conçu pour représenter les informations liées à l’état de départ de divers attributs du lecteur. Elle inclut les propriétés [!UICONTROL Player State Name] qui indiquent l’état spécifique de l’attribut (par exemple, « fullscreen », « mute », « closedCaptioning »). Ce type de données est utilisé pour capturer et décrire les conditions initiales de différents états du lecteur.

![Diagramme de [!UICONTROL List of States Start] type de données.](../images/data-types/list-of-states-start-collection.png)

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Non | Nom de l’état du lecteur. Énumérées : « fullscreen », « mute », « closeCaptioning », « pictureInPicture », « inFocus » avec leurs significations respectives. |

{style="table-layout:auto"}
