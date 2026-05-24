---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;interaction web;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'interaction web
description: Découvrez le type de données du modèle de données d’expérience (XDM) d’interaction web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
TQID: https://experienceleague.adobe.com/PRnfkE6zrOaGl0JFexMIpCMoWM-OIcx7lQcBLUEQq9g
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 184
ht-degree: 3%

---

# Type de données [!UICONTROL Web interaction]

[!UICONTROL Web interaction] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les informations sur les interactions qui se sont produites sur une page web une fois le chargement initial de la page terminé. Il est destiné à enregistrer les interactions dans des applications web riches qui ne déclenchent pas de nouveau chargement de page, telles que les applications web monopages (SPA).

![image de l’interaction web](../images/data-types/web-interaction.PNG){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Measure]](./measure.md) | Mesure assurant le suivi des clics sur un lien web. |
| `URL` | Chaîne | URL ou lien réel utilisé pour cette interaction web. |
| `name` | Chaîne | Nom normatif utilisé pour ce lien web. Il est utilisé à des fins de classification. |
| `type` | Chaîne | Type de lien. Cette propriété doit être égale à l’une des valeurs d’énumération suivantes : <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
