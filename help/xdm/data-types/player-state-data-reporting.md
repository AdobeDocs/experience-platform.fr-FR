---
title: Type de données de création de rapports sur l’état du lecteur
description: Découvrez le type de données XDM (Player State Data Reporting Experience Data Model).
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 21%

---

# [!UICONTROL &#x200B; Type de données &#x200B;] rapport de données sur l’état du lecteur

[!UICONTROL &#x200B; La création de rapports sur les données d’état du lecteur &#x200B;] est un type de données XDM (Experience Data Model) standard qui décrit les différents états et leurs occurrences dans un lecteur multimédia. Utilisez le type de données [!UICONTROL Rapport de données sur l’état du lecteur] pour capturer différents états du lecteur tels que le plein écran, le mode silencieux, le sous-titrage, l’incrustation dans l’image et les états In-Focus. Pour chaque état, il enregistre si l’état est défini, le nombre d’occurrences et la durée totale pendant laquelle il reste actif pendant la lecture multimédia.

![Schéma du type de données de rapport de données de l’état du lecteur.](../images/data-types/player-state-data-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Nom de l’état du lecteur] | `name` | Chaîne | Nom de l’état du lecteur. Énuméré : &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; avec leurs significations respectives. |
| [!UICONTROL Jeu d’états du lecteur] | `isSet` | Booléen | Détermine si le lecteur est défini ou non sur cet état. |
| [!UICONTROL Nombre d’états du lecteur] | `count` | Entier | Nombre de fois que l’état du lecteur a été défini sur le flux. |
| [!UICONTROL Temps d’état du lecteur] | `time` | Entier | Durée totale de cet état de lecteur. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
