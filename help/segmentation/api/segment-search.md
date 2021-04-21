---
keywords: Experience Platform;segmentation;service de segmentation;dépannage;API;seg;segment;Segment;search;segment search;segment search;
title: Point de terminaison de l’API de recherche de segments
topic-legacy: guide
description: Dans l’API Adobe Experience Platform Segmentation Service, la recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Ce guide fournit des informations qui vous aideront à mieux comprendre la recherche de segments et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 44%

---

# Point de terminaison de la recherche de segments

La recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel.

Ce guide fournit des informations qui vous aideront à mieux comprendre la recherche de segments et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de l&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API, y compris les en-têtes requis et pour savoir comment lire des exemples d&#39;appels d&#39;API.

Outre les en-têtes requis décrits dans la section Prise en main, toutes les requêtes envoyées au point de terminaison Recherche de segment nécessitent l’en-tête supplémentaire suivant :

- x-ups-search-version : &quot;1.0&quot;

### Recherche entre plusieurs espaces de nommage

Ce point de terminaison de recherche peut être utilisé pour effectuer des recherches dans divers espaces de nommage, renvoyant une liste de résultats du nombre de recherches. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Paramètres | Description |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoire)** Où {SCHÉMA} représente la valeur de classe de schéma associée aux objets de recherche. Actuellement, seul `_xdm.context.segmentdefinition` est pris en charge. |
| `s={SEARCH_TERM}` | *(Facultatif)* Où {SEARCH_TERM} représente une requête conforme à la mise en oeuvre par Microsoft de la syntaxe [ de recherche de ](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax)Lucene. Si aucun terme de recherche n’est spécifié, tous les enregistrements associés à `schema.name` seront renvoyés. Vous trouverez une explication plus détaillée dans l&#39;[appendice](#appendix) du présent document. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les informations suivantes.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Rechercher des entités individuelles

Ce point de terminaison de recherche peut être utilisé pour récupérer une liste de tous les objets indexés en texte intégral dans l’espace de nommage spécifié. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Paramètres | Description |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoire)** Où {SCHÉMA} contient la valeur de classe de schéma associée aux objets de recherche. Actuellement, seul `_xdm.context.segmentdefinition` est pris en charge. |
| `namespace={NAMESPACE}` | **(Obligatoire)** Où {ESPACE DE NOMMAGE} contient l&#39;espace de nommage dans lequel vous souhaitez effectuer une recherche. |
| `s={SEARCH_TERM}` | *(Facultatif)* Où {SEARCH_TERM} contient une requête conforme à la mise en oeuvre par Microsoft de la syntaxe [ de recherche de ](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si aucun terme de recherche n’est spécifié, tous les enregistrements associés à `schema.name` seront renvoyés. Vous trouverez une explication plus détaillée dans l&#39;[appendice](#appendix) du présent document. |
| `entityId={ENTITY_ID}` | *(Facultatif)* Limite votre recherche au sein du dossier désigné, spécifié avec {ENTITY_ID}. |
| `limit={LIMIT}` | *(Facultatif)* Où {LIMIT} représente le nombre de résultats de recherche à renvoyer. La valeur par défaut est 50. |
| `page={PAGE}` | *(Facultatif)* Où {PAGE} représente le numéro de page utilisé pour paginer les résultats de la requête recherchée. Veuillez noter que le numéro de page est début à **0**. |


**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des résultats correspondant à la requête de recherche.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Obtenir des informations structurelles sur un objet de recherche

Ce point de terminaison de recherche peut être utilisé pour obtenir les informations structurelles sur l&#39;objet de recherche demandé.

**Format d’API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Paramètres | Description |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoire)** Où {SCHÉMA} contient la valeur de classe de schéma associée aux objets de recherche. Actuellement, seul `_xdm.context.segmentdefinition` est pris en charge. |
| `namespace={NAMESPACE}` | **(Obligatoire)** Où {ESPACE DE NOMMAGE} contient l&#39;espace de nommage dans lequel vous souhaitez effectuer une recherche. |
| `entityId={ENTITY_ID}` | **(Obligatoire)** ID de l&#39;objet de recherche dont vous souhaitez obtenir les informations structurelles, spécifié avec {ENTITY_ID}. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 200 avec des informations structurelles détaillées sur l&#39;objet de recherche demandé.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment fonctionne la recherche de segments.

## Annexe {#appendix}

Les sections suivantes fournissent des informations supplémentaires sur le fonctionnement des termes de recherche. Les requêtes de recherche sont rédigées de la manière suivante : `s={FieldName}:{SearchExpression}`. Ainsi, par exemple, pour rechercher un segment nommé AAM ou [!DNL Platform], utilisez la requête de recherche suivante : `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Pour les meilleures pratiques, l’expression de recherche doit être encodée au format HTML, comme l’exemple ci-dessus.

### Champs de recherche {#search-fields}

Le tableau suivant liste les champs qui peuvent être recherchés dans le paramètre de requête de recherche.

| Nom du champ | Description |
| ---------- | ----------- |
| folderId | Dossier ou dossiers dont l’ID de dossier correspond à la recherche spécifiée. |
| folderLocation | Emplacement ou emplacements où se trouve le dossier de la recherche spécifiée. |
| parentFolderId | Le segment ou le dossier dont l’ID de dossier parent est celui de la recherche spécifiée. |
| segmentId | Le segment correspond à l’ID du segment de votre recherche spécifiée. |
| segmentName | Le segment correspond au nom du segment de votre recherche spécifiée. |
| segmentDescription | Le segment correspond à la description du segment de votre recherche spécifiée. |

### Expression de recherche {#search-expression}

Le tableau suivant liste les détails du fonctionnement des requêtes de recherche lors de l&#39;utilisation de l&#39;API de recherche de segment.

>!![NOTE] Les exemples suivants sont présentés dans un format non codé en HTML pour une meilleure clarté. Pour les meilleures pratiques, code HTML pour votre expression de recherche.

| Exemple d&#39;expression de recherche | Description |
| ------------------------- | ----------- |
| foo | Recherche de n’importe quel mot. Cela renverra des résultats si le mot « foo » se trouve dans l’un des champs pouvant faire l’objet d’une recherche. |
| foo AND bar | Recherche booléenne. Cela renverra des résultats si les mots « foo » **et** « bar » se trouvent dans l’un des champs pouvant faire l’objet d’une recherche. |
| foo OR bar | Recherche booléenne. Cela renverra des résultats si le mot « foo » **ou** le mot « bar » se trouve dans l’un des champs pouvant faire l’objet d’une recherche. |
| foo NOT bar | Recherche booléenne. Cela renverra des résultats si le mot « foo » dans l’un des champs pouvant faire l’objet d’une recherche, mais que le mot « bar » ne se trouve dans aucun des champs pouvant faire l’objet d’une recherche. |
| name: foo AND bar | Recherche booléenne. Cela renverra des résultats si les mots « foo » et « bar » se trouvent **tous les deux** dans le champ « name ». |
| run* | Recherche par caractères génériques. L’utilisation d’un astérisque (*) correspond à 0 caractère ou plus, ce qui signifie que cela renverra des résultats si le contenu de l’un des champs pouvant faire l’objet d’une recherche contient un mot commençant par « run ». Par exemple, des résultats sont renvoyés si les mots « run », « running », « runner » ou « runt » apparaissent. |
| cam? | Recherche par caractères génériques. Utilisation d’un point d’interrogation (?) Correspond à un seul caractère, ce qui signifie que cela renverra des résultats si le contenu de l’un des champs pouvant faire l’objet d’une recherche commence par « cam » et une lettre supplémentaire. Par exemple, cela pourra renvoyer « camp » ou « cams », mais pas « camera » ou « campfire ». |
| &quot;blue umbrella&quot; | Recherche d’expression. Cela renverra des résultats si le contenu de l’un des champs pouvant faire l’objet d’une recherche contient l’expression complète « blue umbrella ». |
| blue\~ | Recherche approximative. Vous pouvez éventuellement placer un nombre compris entre 0 et 2 après le signe tilde (~) pour spécifier la distance de modification. Par exemple, « blue\~1 » renvoie « blue », « blues » ou « glue ». La recherche approximative peut **uniquement** être appliquée aux termes, et non aux expressions. Vous pouvez toutefois ajouter des tildes à la fin de chaque mot d’une phrase. Par exemple, « camping\~ in\~ the\~ summer\~ » correspondrait à « camping in the summer ». |
| &quot;hotel airport&quot;\~5 | Recherche de proximité. Ce type de recherche permet de rechercher des termes proches les uns des autres dans un document. Par exemple, l’expression `"hotel airport"~5` trouvera les termes « hotel » et « airport » à moins de 5 mots l’un de l’autre dans un document. |
| `/a[0-9]+b$/` | Recherche avec expressions régulières. Ce type de recherche trouve une correspondance basée sur le contenu entre les barres obliques « / », comme indiqué dans la classe RegExp. Par exemple, pour rechercher des documents contenant « motel » ou « hotel », spécifiez `/[mh]otel/`. Les recherches avec expressions régulières sont comparées à des mots uniques. |

Pour obtenir une documentation plus détaillée sur la syntaxe des requêtes, veuillez lire la [documentation sur la syntaxe Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
