---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;détails de page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données Détails de la page web
description: Découvrez le type de données du modèle de données d’expérience (XDM) relatif aux détails de la page web.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 11%

---

# [!UICONTROL Détails de la page web] type de données

[!UICONTROL Détails de la page web] est un type de données XDM (Experience Data Model) standard qui décrit les détails d’une page web qui vient d’être chargée et affichée, tel qu’enregistré par un ExperienceEvent.

Le type de données est destiné aux détails complets de la page et aux chargements initiaux de pages des applications web d’une seule page (SPA). Pour les interactions qui se produisent sur une page chargée et qui ne déclenchent pas de nouveau chargement de page, consultez le type de données [interaction web](./web-interaction.md) .

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Mesure]](./measure.md) | Nombre de vues sur une page web. |
| `URL` | Chaîne | URL normative ou habituelle de la page web. Il peut s’agir de l’URL réelle utilisée pour atteindre la page. Pour enregistrer l’URL utilisée pour atteindre la page, utilisez `webLink`. Le format URI doit respecter la norme [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booléen | Cette propriété utilise un indicateur pour indiquer si la page est une page d’erreur ou non. Cet indicateur est utilisé pour classer les interactions web de manière générale. L&#39;erreur est définie par l&#39;application et peut correspondre à une page diffusée avec un code d&#39;erreur HTTP. |
| `isHomePage` | Booléen | Cette propriété utilise un indicateur pour indiquer si la page est une page d’accueil ou non. Cet indicateur est utilisé pour classer les interactions web de manière générale. La définition de la page d’accueil est déterminée par l’application. |
| `name` | Chaîne | Nom normatif de la page web. Il ne s’agit pas nécessairement du titre de la page et il n’est pas nécessairement associé directement au contenu de la page. Cependant, il est utilisé pour organiser les pages d’un site à des fins de classification. |
| `server` | Chaîne | Serveur normatif ou habituel qui héberge la page web. Il peut s’agir de l’hôte ou du serveur qui a réellement servi l’interaction de la page. |
| `siteSection` | Chaîne | Nom normatif de la section du site où se trouve cette page web. Vous pouvez l’utiliser pour classer ou catégoriser l’interaction. |
| `viewName` | Chaîne | Nom de la vue, dans une page. Cette propriété est généralement utilisée avec les applications d’une seule page ou les pages qui comportent des onglets ou des contrôles qui modifient la plupart de la mise en page. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
