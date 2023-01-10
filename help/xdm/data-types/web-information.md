---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;détails de page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données des informations web
description: Ce document fournit un aperçu du type de données XDM (Experience Data Model), informations web.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 13%

---

# [!UICONTROL Informations web] type de données

[!UICONTROL Informations web] est un type de données XDM (Experience Data Model) standard qui décrit les informations enregistrées via un événement d’expérience spécifique au canal World Wide Web, y compris la page web, le référent et/ou le lien associé à l’interaction sur la page.

![](../images/data-types/web-information.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Interaction web]](./web-interaction.md) | Décrit les détails du lien web ou de l’URL qui correspond à l’interaction. |
| `webPageDetails` | [[!UICONTROL Informations sur la page web]](./webpage-details.md) | Décrit les détails de la page web sur laquelle l’interaction web s’est produite. |
| `webReferrer` | [!UICONTROL Objet] | Décrit le référent d’une interaction web, c’est-à-dire l’URL d’origine d’un visiteur juste avant l’enregistrement de l’interaction web actuelle. Contient les sous-propriétés suivantes : <ul><li>`URL`: URL du référent.</li><li>`type`: Type de référent.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
