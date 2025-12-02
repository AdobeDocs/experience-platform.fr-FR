---
title: environment
description: Environnement de création actuellement utilisé par la propriété de balise.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 6%

---

# `environment`

L’objet `_satellite.environment` indique l’environnement de création actuellement utilisé par la propriété de balise.

```js
readonly _satellite.environment: Environment
```

## Champs disponibles

Les champs suivants sont disponibles lors de l’appel de cet objet.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Nom | Type | Description |
|---|---|---|
| **`id`** | `string` | Identifiant unique de l’environnement. Vous pouvez localiser l’identifiant d’environnement en sélectionnant l’icône **[!UICONTROL Install]** sous [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) dans l’interface utilisateur des balises. |
| **`stage`** | `development \| staging \| production` | Type d’environnement. |
