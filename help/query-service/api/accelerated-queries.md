---
title: Point d’entrée de requêtes accélérées
description: Découvrez comment accéder sans état à la boutique accélérée de requêtes pour renvoyer rapidement des résultats basés sur des données agrégées. Ce document fournit un exemple de requête HTTP et de réponse pour le point d’entrée de requêtes accélérées de Query Service.
role: Developer
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 97%

---

# Point d’entrée de requêtes accélérées

Dans le cadre du SKU Data Distiller, l’[API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/) vous permet d’effectuer des requêtes sans état vers la boutique accélérée. Les résultats renvoyés sont basés sur des données agrégées. La diminution de la latence des résultats permet un échange plus interactif d’informations. Les API de requêtes accélérées sont également utilisées pour alimenter les [tableaux de bord définis par l’utilisateur](../../dashboards/standard-dashboards.md).

Avant de poursuivre avec ce guide, assurez-vous d’avoir lu et compris le [guide de l’API Query Service](./getting-started.md) pour utiliser correctement l’API Query Service.

## Prise en main

Le SKU Data Distiller est requis pour utiliser la boutique de requêtes accélérées. Veuillez consulter la documentation [packaging](../packaging.md) et [guardrails](../guardrails.md#query-accelerated-store), ainsi que la documentation [licensing](../data-distiller/license-usage.md) relative au SKU de Data Distiller. Si vous ne disposez pas du SKU de Data Distiller, contactez votre représentant du service client Adobe pour plus d’informations.

Les sections suivantes détaillent les appels d’API nécessaires pour accéder sans état à la boutique de requêtes accélérées via l’API Query Service. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

## Exécuter une requête accélérée {#run-accelerated-query}

Envoyez une requête POST au point d’entrée `/accelerated-queries` pour exécuter une requête accélérée. La requête est contenue directement dans la payload de la requête ou référencée avec un identifiant de modèle.

**Format d’API**

```shell
POST /accelerated-queries
```

### Requête

>[!IMPORTANT]
>
>Les requêtes au point d’entrée `/accelerated-queries` nécessitent une instruction SQL OU un identifiant de modèle, mais pas les deux. L’envoi des deux dans une requête provoque une erreur.

La requête suivante envoie une requête SQL dans le corps de la requête à la boutique accélérée.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Cette autre requête envoie un identifiant de modèle dans le corps de la requête à la boutique accélérée. Le code SQL du modèle correspondant est utilisé pour envoyer une requête à la boutique accélérée.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Propriété | Description |
|---|---|
| `dbName` | Nom de la base de données vers laquelle vous effectuez une requête accélérée. La valeur de `dbName` doit prendre le format `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. La base de données fournie doit exister dans la boutique accélérée, sinon la requête entraînera une erreur. Vous devez également vous assurer que l’en-tête `x-sandbox-name` et le nom du sandbox dans `dbName` se rapportent au même sandbox. |
| `sql` | Chaîne d’instruction SQL. La taille maximale autorisée est de 1 000 000 caractères. |
| `templateId` | L’identifiant unique d’une requête créée et enregistrée en tant que modèle lorsqu’une demande POST est envoyée au point d’entrée `/templates`. |
| `name` | Nom descriptif et convivial facultatif pour la requête accélérée. |
| `description` | Commentaire facultatif sur l’intention de la requête pour aider d’autres utilisateurs à comprendre son objectif. La taille maximale autorisée est de 1 000 octets. |

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec le schéma ad hoc créé par la requête.

>[!NOTE]
>
>La réponse suivante a été tronquée pour des raisons de concision.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Propriété | Description |
|---|---|
| `queryId` | La valeur de l’identifiant de la requête créée. |
| `resultsMeta` | Cet objet contient les métadonnées pour chaque colonne renvoyée dans les résultats afin que les utilisateurs et utilisatrices connaissent le nom et le type de chaque colonne. |
| `resultsMeta._adhoc` | Schéma de modèle de données d’expérience (XDM) ad hoc avec des champs dont l’espace de nom est réservé à une utilisation par un seul jeu de données. |
| `resultsMeta._adhoc.type` | Type de données du schéma ad hoc. |
| `resultsMeta._adhoc.meta:xdmType` | Il s’agit d’une valeur générée par le système pour le type de champ XDM. Pour plus d’informations sur les types disponibles, consultez la documentation sur les [types XDM disponibles](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | Il s’agit des noms des colonnes du jeu de données interrogé. |
| `resultsMeta._adhoc.results` | Il s’agit des noms des lignes du jeu de données interrogé. Ils reflètent chacune des colonnes renvoyées. |
