---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;Détails de la page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données d'informations Web
description: Découvrez le type de données des modèles de données d’expérience (XDM) d’informations web.
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
TQID: https://experienceleague.adobe.com/8VirJ2uuFLnH0-JFMtcqXs7mkhSTcD1Skr1L3VM5QsM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 176
ht-degree: 2%

---

# Type de données [!UICONTROL Web information]

[!UICONTROL Web information] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les informations enregistrées via un événement d’expérience spécifique au canal World Wide Web, y compris la page web, le référent et/ou le lien associé à l’interaction sur la page.

![](../images/data-types/web-information.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web interaction]](./web-interaction.md) | Décrit les détails sur le lien web ou l’URL qui correspond à l’interaction. |
| `webPageDetails` | [[!UICONTROL Web page details]](./webpage-details.md) | Décrit les détails sur la page web où s’est produite l’interaction web. |
| `webReferrer` | [!UICONTROL Object] | Décrit le référent d’une interaction web, qui est l’URL de provenance du visiteur juste avant l’enregistrement de l’interaction web actuelle. Contient les sous-propriétés suivantes : <ul><li>`URL` : URL du référent.</li><li>`type` : type de référent.</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
