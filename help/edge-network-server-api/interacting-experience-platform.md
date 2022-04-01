---
title: Interaction avec Adobe Experience Platform
description: Découvrez comment utiliser l’API Edge Network Server pour interagir avec Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: la collecte de données; le point d'exutoire; les analyses; API réseau Adobe Experience Platform Edge, aep
source-git-commit: 1880f391b3276aa61d0c94c1567f2dd555b66edc
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# Interaction avec Adobe Experience Platform

## Présentation {#overview}

Pour activer la collecte de données Experience Platform, vous devez d’abord [configuration de votre flux de données](../edge/fundamentals/datastreams.md) pour transférer des événements dans des jeux de données Experience Platform.

Une fois configurée, la configuration du flux de données doit inclure des paramètres pour `com_adobe_experience_platform`, comme illustré dans l’exemple ci-dessous :


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
