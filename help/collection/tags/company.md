---
title: entreprise
description: Obtenez des informations sur l’organisation IMS propriétaire de la propriété de balise implémentée.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

L’objet `_satellite.company` affiche des informations sur l’organisation IMS propriétaire de la propriété de balise.

```ts
readonly _satellite.company: Company
```

## Champs disponibles

Les champs suivants sont disponibles lors de l’appel de cet objet :

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Nom | Type | Description |
| --- | --- | --- |
| **`orgId`** | `string` | Identifiant d’organisation IMS de la propriété de balise. |
| **`dynamicCdnEnabled`** | `boolean` | Détermine si votre propriété de balise utilise la fonctionnalité de changement de réseau CDN dynamique d’Adobe. Si la valeur est définie sur `true`, le réseau CDN à partir duquel un visiteur demande votre balise bascule automatiquement en fonction de son emplacement. |
| **`cdnAllowList`** | `string[]` | Les réseaux de diffusion de contenu autorisés à charger votre propriété de balise. |

Des informations similaires sont également contenues dans `_satellite._container.company`. Voir [`_container`](container.md) pour plus d’informations.
