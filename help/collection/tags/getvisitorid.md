---
title: getVisitorId
description: Récupérez l’instance d’extension de balise du service d’identification des visiteurs.
exl-id: ecfd4325-1881-47a9-bc3c-abfc780ce52f
TQID: https://experienceleague.adobe.com/QphQk2-krztWgDLMsnqrcOVsWPleioQMEDRplRDp1LY
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 2f54212d8592c5ebc45b847c5f8269ddddfeb622
workflow-type: tm+mt
source-wordcount: 221
ht-degree: 4%

---

# `getVisitorId()`

La méthode `_satellite.getVisitorId()` renvoie une instance du [service d’identification des visiteurs](https://experienceleague.adobe.com/fr/docs/id-service/using/home) dans votre propriété de balise, **si** l’extension « [!UICONTROL service Adobe Experience Cloud ID] » est installée et publiée. Cette méthode s’avère utile lorsque vous souhaitez un accès direct au service d’identification des visiteurs pour une utilisation dans des blocs de code personnalisés, une configuration avancée d’éléments de données ou la résolution de problèmes d’identité des visiteurs.

>[!IMPORTANT]
>
>Cette méthode s’applique uniquement aux propriétés qui incluent l’extension de balise autonome « [!UICONTROL Adobe Experience Cloud ID Service] ». Elle ne s’applique pas aux fonctionnalités d’identité implicite disponibles dans l’extension de balise Web SDK. Voir la commande [`getIdentity`](/help/collection/js/commands/getidentity.md) si vous devez obtenir une identité de visiteur à l’aide des fonctionnalités d’identité implicite de SDK Web.

Si vous appelez cette méthode avec l’extension « [!UICONTROL Adobe Experience Cloud ID Service] » installée et publiée, un objet est renvoyé, similaire à l’objet obtenu après avoir appelé la méthode [`Visitor.getInstance()`](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/getinstance). Si vous appelez cette méthode alors que l’extension de balise « [!UICONTROL Adobe Experience Cloud ID Service] » n’est ni installée ni publiée, la méthode renvoie `null`.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Champs et méthodes disponibles

Consultez la documentation du service d’identification des visiteurs [Méthodes](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/get-set) pour savoir quels champs et méthodes sont disponibles.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
