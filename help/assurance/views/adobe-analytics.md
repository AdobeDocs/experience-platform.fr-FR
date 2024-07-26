---
title: Vue Adobe Analytics dans Assurance
description: Ce guide explique comment utiliser Adobe Analytics avec Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 515f58175a8ccba03581ce4d7faf23fdfed3571e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# Vue Adobe Analytics dans Assurance

>[!IMPORTANT]
>
>La vue d’événements Analytics est consolidée dans le plug-in **Analytics Events 2.0 (Beta)**.  Il sera retiré de l’assurance dans le futur. Nous vous recommandons d’utiliser le **module externe Analytics Events 2.0 (Beta)** pour votre débogage Analytics pour les sessions d’assurance.

L’intégration de Adobe Experience Platform Assurance à Adobe Analytics offre une vue plus riche des événements de SDK aux utilisateurs pour le débogage et la validation de leur mise en oeuvre Adobe Analytics. La vue affiche désormais les événements de cycle de vie et d’action/d’état envoyés à Adobe Analytics à partir du [SDK Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). La vue comprend également des détails de &quot;réponse&quot; qui fournissent des informations sur le traitement des événements après l’application des règles de traitement de chaque suite de rapports respective.

![](./images/adobe-analytics/overview.png)

## Commencer

Avant de poursuivre, assurez-vous que vous disposez des services suivants :

- [Interface utilisateur de collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Pour savoir comment installer Assurance dans votre application, consultez le [guide d’assurance d’implémentation](../tutorials/implement-assurance.md).

## Etat post-traitement

Une fois que le SDK a effectué une requête réseau avec Adobe Analytics, l’état vous indique si Assurance a été en mesure de récupérer les informations de post-traitement pour la requête Adobe Analytics.

Pour récupérer les informations de post-traitement, l’utilisateur connecté doit avoir accès à la suite de rapports correspondante.

| État | Description |
| :----- | :---------- |
| `Queued` | La requête réseau récupère les informations de post-traitement. |
| `Processed` | La requête réseau a réussi et les informations de post-traitement sont reçues. |
| `Delayed` | Le nombre maximal de tentatives de récupération des informations de post-traitement a été dépassé. |
| `Error` | Une erreur provoquait l’échec de la requête réseau. Des informations supplémentaires sur l’erreur s’affichent dans la vue des détails de l’événement. |
| `Unauthorized` | L’utilisateur n’a pas accès à la suite de rapports Adobe Analytics. |
| `Unavailable` | La requête Adobe Analytics ne comporte pas d’événement `AnalyticsResponse` correspondant. |
| `No Debug Flag` | La version actuelle du SDK Adobe Analytics ou Assurance peut ne pas prendre en charge la fonctionnalité de débogage Analytics. Pour plus d’informations, consultez le [guide de dépannage](../troubleshooting.md). |
| `Expired` | L’événement `AnalyticsTrack` ou `LifecycleStart` a plus de 24 heures. |

## Affichage des détails de l’événement

Pour un événement de suivi Analytics, la vue détaillée contient les éléments importants suivants :

- Événement de demande d’Analytics du SDK d’origine.
- Métadonnées et données contextuelles prêtes à l’emploi de la requête, telles que l’identifiant de la suite de rapports, les versions de l’extension SDK, les données contextuelles prêtes à l’emploi, etc.
- Informations post-traitées sur l’événement Analytics qui contient le mappage des variables, evars, props, etc.
