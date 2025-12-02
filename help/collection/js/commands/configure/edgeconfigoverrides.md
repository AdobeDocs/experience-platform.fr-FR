---
title: edgeConfigOverrides
description: Configurez les remplacements de train de données pour votre implémentation.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (commande `configure`)

L’objet `edgeConfigOverrides` vous permet de remplacer les paramètres de configuration pour les commandes exécutées sur la page active. Cet objet est utile lorsque vous disposez de sites web ou de sous-domaines différents pour différents pays ou si vous disposez de plusieurs sandbox Experience Platform pour stocker des données spécifiques à différentes unités commerciales. Si vous souhaitez remplacer les paramètres de configuration pour une seule commande de la page, pensez à utiliser l’objet [`edgeConfigOverrides` dans la commande `sendEvent`](../sendevent/edgeconfigoverrides.md).

Le processus de remplacement de la configuration des trains de données comprend deux étapes principales :

1. Tout d’abord, vous devez définir le remplacement de votre configuration de train de données lors de la [configuration d’un train de données](/help/datastreams/configure.md) dans l’interface utilisateur des trains de données. Consultez [Remplacements de la configuration des trains de données](/help/datastreams/overrides.md) dans la documentation sur les trains de données pour obtenir des instructions sur la configuration des remplacements.
1. Après avoir configuré le remplacement du flux de données dans l’interface utilisateur des flux de données, vous pouvez configurer l’objet `edgeConfigOverrides`.

Lorsque vous définissez l’objet `edgeConfigOverrides` dans la commande `configure`, il s’applique à toutes les données envoyées à Adobe. Les commandes suivantes _également_ prennent en charge l’objet `edgeConfigOverrides` :

* [`sendEvent`](../sendevent/edgeconfigoverrides.md)
* [`setConsent`](../setconsent.md)
* [`getIdentity`](../getidentity.md)
* [`appendIdentityToUrl`](../appendidentitytourl.md)

La définition de `edgeConfigOverrides` dans l’une des commandes ci-dessus est prioritaire sur l’objet `edgeConfigOverrides` dans la commande `configure` si les deux sont définis. Si l’une de ces commandes ne contient pas d’objet `edgeConfigOverrides`, l’objet `edgeConfigOverrides` de la commande `configure` est utilisé.

## Exemple

Si tous les services pris en charge sont activés pour votre configuration de train de données, l’exemple ci-dessous remplace ce paramètre et désactive tous les services.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Paramètre | Type | Description |
| --- | --- | --- |
| **`orgId`** | `string` | L’identifiant d’organisation IMS de votre entreprise. |
| **`datastreamId`** | `string` | Identifiant du flux de données auquel envoyer des données. |
| **`com_adobe_experience_platform`** | `object` | Définit la configuration du flux de données dynamique pour les services Adobe Experience Platform. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Détermine si l’événement est envoyé à Adobe Experience Platform. |
| **`com_adobe_experience_platform.datasets`** | `object` | Définit les jeux de données utilisés pour l’événement. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Détermine si l’événement est envoyé à Offer Decisioning. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Détermine si l’événement est envoyé à la segmentation Edge. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Détermine si l’événement est envoyé aux destinations Edge. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Détermine si l’événement est envoyé au Adobe Journey Optimizer. |
| **`com_adobe_analytics.enabled`** | `boolean` | Détermine si l’événement est envoyé à Adobe Analytics. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Tableau de chaînes qui détermine les suites de rapports auxquelles envoyer des données Analytics. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Détermine si l’événement est envoyé à Adobe Audience Manager. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | Conteneur de synchronisation des identifiants tiers à utiliser dans Audience Manager. Nécessite `com_adobe_audience_manager.enabled` définir sur `true`. Dans le cas contraire, le service Audience Manager est désactivé. |
| **`com_adobe_target.enabled`** | `boolean` | Détermine si l’événement est envoyé à Adobe Target. |
| **`com_adobe_target.propertyToken`** | `string` | Jeton de la propriété de destination Adobe Target. |
| **`com_adobe_launch_ssf`** | `boolean` | Détermine si l’événement est envoyé au transfert côté serveur. |

## Remplacements de configuration à l’aide de l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de ce champ se trouve sous [ Remplacements de configuration ](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) lors de la configuration de l’extension de balise.
