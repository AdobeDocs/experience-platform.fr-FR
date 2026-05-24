---
title: eventType
description: Définissez le type d’événement pour un appel sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
TQID: https://experienceleague.adobe.com/amcl11k32moRYEd4dOehhKhspTvDOclDEm1iHvdLbSo
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 0%

---

# `eventType`

La propriété `eventType` vous permet de définir le type d’événement que vous envoyez à l’aide du SDK Web. Ce champ renseigne finalement le champ `xdm.eventType`. Il s’avère utile lorsque vous souhaitez différencier les types d’événements que vous envoyez à Adobe.

Adobe fournit certains types d’événements prédéfinis que vous pouvez utiliser. Consultez [&#x200B; Valeurs disponibles pour `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) dans le guide d’utilisation XDM pour obtenir une liste complète des valeurs prédéfinies. Vous pouvez également utiliser vos propres valeurs si vous le souhaitez.

Si vous définissez les deux `type` ici et `xdm.eventType` dans l’objet [`xdm`](xdm.md), la valeur de ce champ est prioritaire.

Définissez la propriété de chaîne `eventType` lors de l’exécution de la commande `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Type d’événement utilisant l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de cette propriété est le menu déroulant [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) lors de la configuration d’une action « [!UICONTROL Send event] ».
