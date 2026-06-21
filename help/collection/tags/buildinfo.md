---
title: buildInfo
description: Obtenez des informations sur la version de balise implémentée sur votre site.
exl-id: 1bf9918c-aeb2-4c40-a166-25d209458aec
source-git-commit: 2d7ba15f918c314fe219212df82aec6d7ac1fc77
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 2%

---

# `buildInfo`

L’objet `_satellite.buildInfo` contient des informations sur la version de la propriété de balise implémentée. Cet objet est particulièrement utile lors du débogage de builds fréquents pour vous assurer que vous utilisez la dernière version.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Champs disponibles

Les champs suivants sont disponibles lors de l’appel de cet objet.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Nom | Type | Description |
| --- | --- | --- |
| **`minified`** | `boolean` | Indique si la bibliothèque est minimisée. Les versions de production sont généralement minimisées (`true`), contrairement aux versions de développement et d’évaluation (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | Date et heure auxquelles votre fichier JavaScript a été créé et publié. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine) est un moteur d’Adobe qui traite les règles de balises et délègue la logique aux extensions de balises. Ce champ contient la date et l’heure de la version de Turbine utilisée pour publier votre propriété de balise. |
| **`turbineVersion`** | `string` | Version de Turbine utilisée pour créer et publier votre propriété de balise. |

Des informations similaires sont également contenues dans `_satellite._container.buildInfo`. Voir [`_container`](container.md) pour plus d’informations.
