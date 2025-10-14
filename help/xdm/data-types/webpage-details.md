---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;Détails de la page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données des détails de la page web
description: Découvrez les détails de la page web sur le type de données du modèle de données d’expérience (XDM).
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 11%

---

# [!UICONTROL Détails de la page web] type de données

[!UICONTROL &#x200B; Détails de la page web &#x200B;] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails d’une page web qui vient d’être chargée et consultée, tels qu’enregistrés par un ExperienceEvent.

Le type de données est destiné aux détails complets de la page et aux chargements initiaux de page des applications web monopages (SPA). Pour les interactions qui se produisent sur une page chargée et qui ne déclenchent pas de nouveau chargement de page, reportez-vous à la section Type de données [interaction web](./web-interaction.md).

![détails de la page web](../images/data-types/web-page-details.PNG){width="500"}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Mesure]](./measure.md) | Nombre de vues sur une page web. |
| `URL` | Chaîne | URL normative ou habituelle de la page web. Il peut s’agir ou non de l’URL réelle utilisée pour accéder à la page. Pour enregistrer l’URL utilisée pour accéder à la page, utilisez `webLink`. Le format URI doit respecter la norme [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booléen | Cette propriété utilise un indicateur pour indiquer si la page est une page d’erreur ou non. Cet indicateur est utilisé pour effectuer une catégorisation large des interactions web. L’erreur est définie par l’application et peut correspondre à une page diffusée avec un code d’erreur HTTP. |
| `isHomePage` | Booléen | Cette propriété utilise un indicateur pour indiquer si la page est une page d’accueil ou non. Cet indicateur est utilisé pour effectuer une catégorisation large des interactions web. La définition de la page d’accueil est déterminée par l’application. |
| `name` | Chaîne | Nom normatif de la page web. Il ne s’agit pas nécessairement du titre de la page et il n’est pas nécessairement associé directement au contenu de la page. Cependant, il est utilisé pour organiser les pages d’un site à des fins de classification. |
| `server` | Chaîne | Serveur habituel ou normatif qui héberge la page web. Il peut s’agir ou non de l’hôte ou du serveur qui a diffusé l’interaction de page. |
| `siteSection` | Chaîne | Nom normatif de la section de site où réside cette page web. Vous pouvez l’utiliser pour classer ou catégoriser l’interaction. |
| `viewName` | Chaîne | Nom de la vue, dans une page. Cette propriété est généralement utilisée avec les applications monopages ou les pages qui comportent des onglets ou des contrôles qui modifient une grande partie de la mise en page. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
