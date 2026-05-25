---
title: Présentation du JavaScript côté client des balises (_satellite)
description: Découvrez lʼobjet _satellite côté client et les différentes fonctions quʼil offre dans les balises.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
TQID: https://experienceleague.adobe.com/bs08vc-tsRpXpuffgLrzWxsaJ57YxVUKSzIkpcRSzT4
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 8%

---

# Présentation du JavaScript côté client des balises (`_satellite`)

_Ces pages décrivent comment utiliser l’objet `_satellite`, ce qui vous permet de gérer et de personnaliser votre logique de balise à l’aide de JavaScript. Consultez [Extension de balise Adobe Experience Platform Web SDK](/help/tags/extensions/client/web-sdk/overview.md) pour plus d’informations sur la configuration de votre implémentation dans l’interface utilisateur de la collecte de données._

L’objet `_satellite` expose plusieurs points d’entrée pris en charge qui vous aident à interagir avec la bibliothèque de balises publiée sur votre site. Tous les déploiements de balises exposent `_satellite` si la balise de chargement est implémentée correctement. Il existe plusieurs cas d’utilisation principaux pour cet objet :

* Utilisation dans votre bibliothèque de balises dans des blocs de code personnalisés, ce qui vous donne un accès complet à la bibliothèque de balises elle-même.
* Déboguer l’implémentation déployée dans n’importe quel environnement (développement, évaluation ou production)
* Implémentation directe sur votre site web, ce qui vous permet de contrôler entièrement le déclenchement des événements ou des règles de balises. Pour les nouvelles mises en œuvre, Adobe recommande d’utiliser une stratégie plus flexible comme la couche de données client [Adobe](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Si vous appelez `_satellite` à partir du code de votre site (par exemple, `_satellite.track()`), **protégez chaque appel** afin que votre site ne soit pas étroitement lié à la bibliothèque de balises.
>
>L’utilisation de `_satellite` dans le code personnalisé d’une propriété de balise ou localement dans la console de votre navigateur ne nécessite pas de protection.

## Exemples d’utilisation courants

```js
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
