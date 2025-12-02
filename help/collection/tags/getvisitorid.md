---
title: getVisitorId
description: Récupérez l’instance d’extension de balise de service de l’identifiant visiteur Experience Cloud.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# `getVisitorId()`

La méthode `_satellite.getVisitorId()` renvoie une instance du service d’ID [Adobe Experience Cloud](https://experienceleague.adobe.com/fr/docs/id-service/using/home) dans votre propriété de balise, **si** l’extension du service d’ID est installée et publiée. Cette méthode s’avère utile lorsque vous souhaitez un accès direct à l’instance d’identifiant visiteur pour une utilisation dans des blocs de code personnalisés, une configuration avancée d’élément de données ou la résolution de problèmes d’identité des visiteurs.

>[!IMPORTANT]
>
>Cette méthode s’applique uniquement aux propriétés qui incluent l’extension de balise de service Experience Cloud ID autonome. Elle ne s’applique pas aux fonctionnalités du service d’ID implicite disponibles dans l’extension de balise Web SDK. Voir la commande [`getIdentity`](/help/collection/js/commands/getidentity.md) si vous devez obtenir une identité de visiteur à l’aide des fonctionnalités du service d’ID implicite de SDK Web.

Si vous appelez cette méthode avec l’extension du service d’ID installée et publiée, un objet est renvoyé, similaire à l’objet obtenu après avoir appelé la méthode [`Visitor.getInstance()`](https://experienceleague.adobe.com/fr/docs/id-service/using/id-service-api/methods/getinstance). Si vous appelez cette méthode alors que l’extension du service d’ID n’est ni installée ni publiée, la méthode renvoie `null`.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Champs et méthodes disponibles

Consultez le service Experience Cloud ID [Méthodes](https://experienceleague.adobe.com/fr/docs/id-service/using/id-service-api/methods/get-set) dans la documentation du service d’identification des visiteurs Experience Cloud pour savoir quels champs et méthodes sont disponibles.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
