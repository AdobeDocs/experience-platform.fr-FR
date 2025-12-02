---
title: edgeConfigOverrides
description: Configurez les remplacements de train de données pour la commande sendEvent uniquement.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
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

L’équivalent de l’extension de balise Web SDK de cet objet est la section [ Remplacements de la configuration du flux de données ](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) lors de la configuration de l’action « [!UICONTROL Send event] ».
