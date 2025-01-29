---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;interaction web;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'interaction web
description: Découvrez le type de données du modèle de données d’expérience (XDM) d’interaction web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---

# [!UICONTROL Interaction web] type de données

[!UICONTROL Interaction web] est un type de données standard des modèles de données d’expérience (XDM) qui décrit les informations sur les interactions qui se sont produites sur une page web une fois le chargement initial de la page terminé. Il est destiné à enregistrer les interactions dans des applications web riches qui ne déclenchent pas de nouveau chargement de page, telles que les applications web monopages (SPA).

![image de l’interaction web](../images/data-types/web-interaction.PNG){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Mesure]](./measure.md) | Mesure assurant le suivi des clics sur un lien web. |
| `URL` | Chaîne | URL ou lien réel utilisé pour cette interaction web. |
| `name` | Chaîne | Nom normatif utilisé pour ce lien web. Il est utilisé à des fins de classification. |
| `type` | Chaîne | Type de lien. Cette propriété doit être égale à l’une des valeurs d’énumération suivantes : <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
