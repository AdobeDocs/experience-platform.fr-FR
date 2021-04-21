---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; interaction Web ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données d'interaction Web
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Experience Data Model) d’interaction Web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 4%

---

# [!UICONTROL Type de données ] d&#39;interaction Web

[!UICONTROL Les ] interactions Web sont un type de données XDM (Experience Data Model) standard qui décrit les informations sur les interactions survenues sur une page Web une fois la page chargée initialement. Il est destiné à enregistrer des interactions dans des applications Web enrichies qui ne déclenchent pas un nouveau chargement de page, comme les applications Web d’une seule page (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Mesure]](./measure.md) | Mesure qui suit le clic sur un lien Web. |
| `URL` | Chaîne | Lien ou URL réel utilisé pour cette interaction Web. |
| `name` | Chaîne | Nom normatif utilisé pour ce lien Web. Il est utilisé à des fins de classification. |
| `type` | Chaîne | Type de lien. Cette propriété doit être égale à l’une des valeurs d’énumération suivantes : <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)
