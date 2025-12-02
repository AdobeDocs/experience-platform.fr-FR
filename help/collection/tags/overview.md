---
title: Référence dʼobjet satellite
description: Découvrez lʼobjet _satellite côté client et les différentes fonctions quʼil offre dans les balises.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 13%

---

# `_satellite` référence d’objet

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
// Read and write a temporary data element value
const region = _satellite.getVar('user_region');
_satellite.setVar('promo_code', code);

// Local debugging
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');

// Manually trigger a rule configured in your tag property
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}
```
