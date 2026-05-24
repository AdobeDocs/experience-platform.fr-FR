---
title: Type de données de rapports sur l’état du lecteur
description: Découvrez le type de données Modèle de données d’expérience (XDM) de création de rapports sur l’état du lecteur.
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
TQID: https://experienceleague.adobe.com/jKhITuKOHg5g-WRNVRXvgl5MXNJst9Tp5YJWU3ddB-4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 176
ht-degree: 10%

---

# Type de données [!UICONTROL Player State Data Reporting]

[!UICONTROL Player State Data Reporting] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les différents états et leurs occurrences dans un lecteur multimédia. Utilisez le type de données [!UICONTROL Player State Data Reporting] pour capturer différents états du lecteur, tels que le plein écran, le mode muet, le sous-titrage, l’image dans l’image et les états de mise au point. Pour chaque état, il enregistre si l’état est défini, le nombre d’occurrences et la durée totale pendant laquelle il reste actif pendant la lecture du média.

![Diagramme du type de données Rapport sur les données de l’état du lecteur.](../images/data-types/player-state-data-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player State Name] | `name` | chaîne | Nom de l’état du lecteur. Énumérées : « fullscreen », « mute », « closeCaptioning », « pictureInPicture », « inFocus » avec leurs significations respectives. |
| [!UICONTROL Player State Set] | `isSet` | booléen | Indique si l’état du lecteur est défini sur cet état. |
| [!UICONTROL Player State Count] | `count` | entier | Nombre de fois que l’état du lecteur a été défini sur le flux. |
| [!UICONTROL Player State Time] | `time` | entier | Durée totale de cet état de lecteur. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
