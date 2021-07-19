---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;détails de page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données des informations web
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM (Experience Data Model), informations web.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# [!UICONTROL Type de données ] d’informations web

[!UICONTROL Les ] informations web sont un type de données XDM (Experience Data Model) standard qui décrit les informations enregistrées via un événement d’expérience spécifique au canal World Wide Web, y compris la page web, le référent et/ou le lien associé à l’interaction sur la page.

![](../images/data-types/web-information.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interaction web]](./web-interaction.md) | Décrit les détails du lien web ou de l’URL qui correspond à l’interaction. |
| `webPageDetails` | [[!UICONTROL Détails des pages web]](./webpage-details.md) | Décrit les détails de la page web sur laquelle l’interaction web s’est produite. |
| `webReferrer` | [!UICONTROL Objet] | Décrit le référent d’une interaction web, c’est-à-dire l’URL d’origine d’un visiteur juste avant l’enregistrement de l’interaction web actuelle. Contient les sous-propriétés suivantes : <ul><li>`URL`: URL du référent.</li><li>`type`: Type de référent.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
