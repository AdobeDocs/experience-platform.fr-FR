---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; Détails de la page Web ; type de données ; type de données ; type de données ; page Web
solution: Experience Platform
title: Type de données Détails de la page Web
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Experience Data Model) des détails de la page Web.
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 10%

---

# [!UICONTROL Type de données ] détaillé de la page Web

[!UICONTROL La page Web ] détaille un type de données XDM (Experience Data Model) standard qui décrit les détails d’une page Web qui vient d’être chargée et consultée, tels qu’ils ont été enregistrés par un ExperienceEvent.

Le type de données est destiné aux détails complets de la page et aux chargements initiaux de pages d’applications Web d’une seule page (SPA). Pour les interactions survenant sur une page chargée qui ne déclenchent pas un nouveau chargement de page, voir le type de données [interaction Web](./web-interactions.md).

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Mesure]](./measure.md) | Nombre de vues sur une page Web. |
| `URL` | Chaîne | URL normative ou habituelle de la page Web. Il peut s’agir de l’URL réelle utilisée pour atteindre la page. Pour enregistrer l&#39;URL utilisée pour atteindre la page, utilisez `webLink`. Le format URI doit respecter la norme [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booléen | Cette propriété utilise un indicateur pour indiquer si la page est une page d’erreur ou non. Cet indicateur est utilisé pour classer les interactions web de manière générale. L&#39;erreur est définie par l&#39;application et peut correspondre à une page diffusée avec un code d&#39;erreur HTTP. |
| `isHomePage` | Booléen | Cette propriété utilise un indicateur pour indiquer si la page est une page d&#39;accueil ou non. Cet indicateur est utilisé pour classer les interactions web de manière générale. La définition de la page d&#39;accueil est déterminée par l&#39;application. |
| `name` | Chaîne | Nom normatif de la page Web. Ce nom n&#39;est pas nécessairement le titre de la page ou directement associé au contenu de la page, mais il est utilisé pour organiser les pages d&#39;un site à des fins de classification. |
| `server` | Chaîne | Serveur normatif ou habituel qui héberge la page web. Il peut s’agir de l’hôte ou du serveur qui a réellement servi l’interaction de page. |
| `siteSection` | Chaîne | Nom normatif de la section du site où se trouve cette page Web. Vous pouvez l’utiliser pour classer ou classer l’interaction. |
| `viewName` | Chaîne | Nom de la vue, dans une page. Cette propriété est généralement utilisée avec les applications d’une seule page ou les pages qui comportent des onglets ou des contrôles qui modifient la majorité de la mise en page. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
