---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conversions PQL
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 5%

---


# Conversions PQL

intro

- Convertir la mise en forme à partir de pql/text et pql/json

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API de segmentation. Avant de continuer, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [Prise en main de la](./getting-started.md#getting-started) sectiondu guide du développeur de segmentation contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Convertir la mise en forme à partir de pql/text et pql/json

**Format d’API**

```http
POST /segment/conversion
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom unique de la définition de segment. |
| `expression.type` | Type d’expression. Cela peut être `PQL` ou `ARL`. |
| `expression.format` | Format d’expression. Cela peut être `pql/text` ou `pql/json`. |
| `expression.value` | Chaîne de requête de l’expression à convertir. |
| `schema.name` | ID de classe du schéma référencé. |
| `ttlInDays` | Entier représentant l’heure de vie (TTL). |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de votre segment converti.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Étapes suivantes
