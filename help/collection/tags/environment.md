---
title: environment
description: Environnement de création actuellement utilisé par la propriété de balise.
exl-id: 9e9873d8-3f86-4ff9-85d0-88670072b7e3
TQID: https://experienceleague.adobe.com/RR5wofWuRY8XV1IdHg6RaoO0jPWTKss8hU-O9swbEME
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 61
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
