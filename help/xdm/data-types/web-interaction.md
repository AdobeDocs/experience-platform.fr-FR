---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;interaction web;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’interaction web
description: Ce document présente l’interaction web du type de données XDM (Experience Data Model).
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 11%

---

# [!UICONTROL Interaction web] type de données

[!UICONTROL Interaction web] est un type de données XDM (Experience Data Model) standard qui décrit les informations sur les interactions qui se sont produites sur une page web une fois le chargement initial de la page terminé. Il est destiné à enregistrer les interactions dans des applications web enrichies qui ne déclenchent pas de nouveau chargement de page, telles que les applications web d’une seule page (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Mesure]](./measure.md) | Mesure qui effectue le suivi des clics sur un lien web. |
| `URL` | Chaîne | Lien ou URL réel utilisé pour cette interaction web. |
| `name` | Chaîne | Nom normatif utilisé pour ce lien web. Il est utilisé à des fins de classification. |
| `type` | Chaîne | Type de lien. Cette propriété doit être égale à l’une des valeurs d’énumération suivantes : <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
