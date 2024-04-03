---
title: Type de données de création de rapports sur l’état du lecteur
description: Découvrez le type de données XDM (Player State Data Reporting Experience Data Model).
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 5%

---

# [!UICONTROL Rapports sur les données d’état du lecteur] type de données

[!UICONTROL Rapports sur les données d’état du lecteur] est un type de données XDM (Experience Data Model) standard qui décrit les différents états et leurs occurrences dans un lecteur multimédia. Utilisez la variable [!UICONTROL Rapports sur les données d’état du lecteur] type de données pour capturer différents états du lecteur, tels que le mode plein écran, le mode muet, le sous-titrage, l’incrustation dans l’image et les états In-Focus. Pour chaque état, il enregistre si l’état est défini, le nombre d’occurrences et la durée totale pendant laquelle il reste actif pendant la lecture multimédia.

![Diagramme du type de données de rapport de données sur l’état du lecteur.](../images/data-types/player-state-data-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Nom de l’état du lecteur] | `name` | Chaîne | Nom de l’état du lecteur. Énuméré : &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; avec leurs significations respectives. |
| [!UICONTROL Jeu d’états du lecteur] | `isSet` | Booléen | Indique si l’état du lecteur est défini sur cet état. |
| [!UICONTROL Nombre d’états du lecteur] | `count` | Entier | Nombre de fois où cet état du lecteur a été défini sur le flux. |
| [!UICONTROL Heure d’état du lecteur] | `time` | Entier | Durée totale de l’état du lecteur. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
