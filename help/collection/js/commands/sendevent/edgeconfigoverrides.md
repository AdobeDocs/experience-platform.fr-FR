---
title: edgeConfigOverrides
description: Configurez les remplacements de train de données pour la commande sendEvent uniquement.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
TQID: https://experienceleague.adobe.com/bkTUWKjT3bqk90h84rGEeR2Uic8UHJwoWJaEkG-BrEg
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: c93393a4-e558-47e1-992e-c91ed4d480ceid: d556b755-390a-43f0-be32-a08cf6236126id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 229
ht-degree: 0%

---

# `edgeConfigOverrides` (commande `sendEvent`)

L’objet `edgeConfigOverrides` vous permet de remplacer les paramètres de configuration uniquement pour la commande `sendEvent` active. Cet objet est utile lorsque la page contient des commandes spécifiques que vous souhaitez exécuter avec des paramètres de configuration différents de ceux du reste de votre implémentation de Web SDK. Si vous souhaitez remplacer les paramètres de configuration pour toutes les commandes d’une page donnée, pensez à utiliser l’objet [`edgeConfigOverrides` dans la commande `configure`](../configure/edgeconfigoverrides.md).

Le processus de remplacement de la configuration du train de données global se compose de deux étapes principales :

1. Tout d’abord, vous devez définir le remplacement de votre configuration de train de données lors de la [configuration d’un train de données](/help/datastreams/configure.md) dans l’interface utilisateur des trains de données. Consultez [Remplacements de la configuration des trains de données](/help/datastreams/overrides.md) dans la documentation sur les trains de données pour obtenir des instructions sur la configuration des remplacements.
1. Après avoir configuré le remplacement du flux de données dans l’interface utilisateur des flux de données, vous pouvez configurer l’objet `edgeConfigOverrides`.

Notez que la commande `configure` prend également en charge un objet `edgeConfigOverrides` ; voir [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) sous la commande `configure`. L’objet `edgeConfigOverrides` de la commande `sendEvent` est prioritaire sur l’objet `edgeConfigOverrides` de la commande `configure` si les deux sont définis.

## Exemple

Si tous les services pris en charge sont activés pour la configuration de votre flux de données, l’exemple ci-dessous remplace ce paramètre et désactive tous les services (voir le paramètre `enabled: false` pour chaque service). Cet objet prend en charge les mêmes propriétés que l’objet [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) dans la commande `configure`.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## Remplacements de la configuration des trains de données à l’aide de l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de cet objet est la section [ Remplacements de la configuration des flux de données ](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) lors de la configuration de l’action « [!UICONTROL Envoyer l’événement] ».
