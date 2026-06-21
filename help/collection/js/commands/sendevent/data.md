---
title: data
description: Découvrez comment envoyer des données non-XDM à Adobe, par le biais de l’objet de données.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
TQID: https://experienceleague.adobe.com/42nSK16mE8kHI8pGzqHNlRgZl-XdvVP-wDrJAzosroU
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a8b0238e-1d43-4679-a3b4-5ba1bad83baa
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---

# `data`

L’objet `data` vous permet d’envoyer à Adobe une payload qui ne correspond pas à un schéma XDM. Elle est utile dans les scénarios non XDM, comme l’envoi direct de données à Adobe Analytics, Adobe Target ou Adobe Audience Manager. Lorsque les données arrivent dans le flux de données, vous pouvez utiliser le [mappage de la préparation des données](/help/data-prep/ui/mapping.md) pour affecter des champs XDM à chaque champ de l’objet `data`. Si un produit est déjà configuré par Adobe pour détecter des champs dans l’objet `data`, vous pouvez envoyer ces données en l’état à un flux de données.

>[!IMPORTANT]
>
>Les données de cet objet doivent avoir au moins l’une des actions suivantes :
>
>* Un service dans le flux de données doit être configuré pour récupérer les données d’une propriété donnée dans l’objet `data`.
>* La propriété donnée doit être mappée à un champ XDM à l’aide de la préparation des données.
>
>Si une propriété donnée n’est pas mappée à un champ XDM ou utilisée par un service configuré, ces données sont définitivement perdues.

Définissez l’objet `data` dans le cadre de l’objet JSON dans le paramètre de la commande `sendEvent`. Pour les données que vous prévoyez de mapper dans le flux de données, vous pouvez structurer cet objet comme vous le souhaitez. Pour les données utilisées par certains services, assurez-vous que la hiérarchie d’objets correspond à ce que le service attend. Vous pouvez inclure l’objet `data` et l’objet [`xdm`](xdm.md) dans la même commande `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Utiliser l’objet `data` avec Adobe Analytics {#analytics}

Vous pouvez utiliser l’objet `data` avec Adobe Analytics pour envoyer des données à une suite de rapports sans schéma XDM. Les variables sont configurées pour utiliser la même syntaxe que les variables AppMeasurement, ce qui simplifie le processus de mise à niveau vers le SDK Web. Voir [&#x200B; Mappage des variables d’objet de données à Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) dans le guide de mise en œuvre d’Adobe Analytics pour plus d’informations.

## Utiliser l’objet `data` à l’aide de l’extension de balise Web SDK

L’objet `data` est disponible en tant qu’élément de données [Variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) lors de l’utilisation de l’extension de balise Web SDK.
