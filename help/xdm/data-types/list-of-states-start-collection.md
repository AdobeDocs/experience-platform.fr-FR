---
title: Type de données de collecte de début de la liste des états
description: Découvrez le type de données Modèle de données d’expérience (XDM) de type Liste d’états démarrés .
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
TQID: https://experienceleague.adobe.com/fr4TJgxCJYOVSKHbWpyGDsmupivHPCCyDY7UXaxRU3Y
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 177
ht-degree: 5%

---

# [!UICONTROL Type de données Début de la liste &#x200B;] états

Le type de données [!UICONTROL Liste d’états Début] est un type de données de modèle de données d’expérience (XDM) conçu pour représenter les informations relatives à l’état de départ de divers attributs du lecteur. Elle inclut la propriété [!UICONTROL Nom de l’état du lecteur] qui indique l’état spécifique de l’attribut (par exemple, « fullscreen », « mute », « closedCaptioning »). Ce type de données est utilisé pour capturer et décrire les conditions initiales de différents états du lecteur.

![Diagramme de type de données [!UICONTROL Début de la liste des états].](../images/data-types/list-of-states-start-collection.png)

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [!UICONTROL Nom de l’état du lecteur] | `name` | string | Non | Nom de l’état du lecteur. Énumérées : « fullscreen », « mute », « closeCaptioning », « pictureInPicture », « inFocus » avec leurs significations respectives. |
