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
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 282
ht-degree: 6%

---

# [!UICONTROL Rapport sur les données de l’état du lecteur] type de données

[!UICONTROL Rapport sur les données d’état du lecteur] est un type de données standard des modèles de données d’expérience (XDM) qui décrit les différents états et leurs occurrences dans un lecteur multimédia. Utilisez le type de données [!UICONTROL Rapports sur les données d’état du lecteur] pour capturer différents états du lecteur, tels que le plein écran, le muet, le sous-titrage, l’image dans l’image et les états de mise au point. Pour chaque état, il enregistre si l’état est défini, le nombre d’occurrences et la durée totale pendant laquelle il reste actif pendant la lecture du média.

![Diagramme du type de données Rapport sur les données de l’état du lecteur.](../images/data-types/player-state-data-information.png)

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaReporting` : champs calculés par le serveur principal des médias en flux continu à partir des données `mediaCollection` envoyées par votre implémentation. Il s’agit des champs qu’Adobe ingère dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

| Nom d’affichage | Propriété | Type de données | Description |
|---|---|---|---|
| [!UICONTROL Nom de l’état du lecteur] | `name` | chaîne | Nom de l’état du lecteur. Énuméré : « fullScreen » (le lecteur occupe le plein écran), « mute » (l’audio est réduit au silence), « closedCaptioning » (les sous-titres sont actifs), « pictureInPicture » (le lecteur est dans un recouvrement flottant), « inFocus » (le lecteur a l’attention active de la visionneuse, généralement parce que l’onglet ou la fenêtre du lecteur est au premier plan). |
| [!UICONTROL État du lecteur défini] | `isSet` | booléen | Indique si l’état du lecteur est défini sur cet état. |
| [!UICONTROL Nombre d’états du lecteur] | `count` | entier | Nombre de fois que l’état du lecteur a été défini sur le flux. |
| [!UICONTROL Heure d’état du lecteur] | `time` | integer | Durée totale de cet état de lecteur, en secondes. |

Voir [playerstatedata.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json) dans le référentiel XDM public pour obtenir la définition complète du schéma.
