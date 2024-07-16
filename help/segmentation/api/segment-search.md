---
title: Point de terminaison de l’API de recherche de segments
description: Dans l’API Adobe Experience Platform Segmentation Service, la recherche de segments est utilisée pour rechercher les champs contenus dans diverses sources de données et les renvoyer en temps quasi réel. Ce guide fournit des informations pour vous aider à mieux comprendre la recherche de segments et inclut des exemples d’appels API pour effectuer des actions de base à l’aide de l’API.
role: Developer
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 44%

---

# Point de terminaison de la recherche de segments

La recherche de segments permet de rechercher des champs contenus dans diverses sources de données et de les renvoyer en temps quasi réel.

Ce guide fournit des informations pour vous aider à mieux comprendre la recherche de segments et inclut des exemples d’appels API pour effectuer des actions de base à l’aide de l’API.

## Commencer

Les points de terminaison utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et comment lire des exemples d’appels API.

Outre les en-têtes requis décrits dans la section Prise en main , toutes les requêtes envoyées au point de terminaison de recherche de segments nécessitent l’en-tête supplémentaire suivant :

- x-ups-search-version: &quot;1.0&quot;

### Recherche parmi plusieurs espaces de noms

Ce point de terminaison de recherche peut être utilisé pour effectuer des recherches dans différents espaces de noms, renvoyant une liste de résultats du nombre de recherches. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Paramètres | Description |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoire)** Où {SCHEMA} représente la valeur de classe de schéma associée aux objets de recherche. Actuellement, seul `_xdm.context.segmentdefinition` est pris en charge. |
| `s={SEARCH_TERM}` | *(Facultatif)* Où {SEARCH_TERM} représente une requête conforme à l’implémentation Microsoft de la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Si aucun terme de recherche n’est spécifié, tous les enregistrements associés à `schema.name` seront renvoyés. Vous trouverez une explication plus détaillée dans l&#39;[annexe](#appendix) de ce document. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

### Recherche d’entités individuelles

Ce point de terminaison de recherche peut être utilisé pour récupérer une liste de tous les objets indexés en texte intégral dans l’espace de noms spécifié. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Paramètres | Description |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoire)** Où {SCHEMA} contient la valeur de classe de schéma associée aux objets de recherche. Actuellement, seul `_xdm.context.segmentdefinition` est pris en charge. |
| `namespace={NAMESPACE}` | **(Obligatoire)** Où {NAMESPACE} contient l’espace de noms dans lequel vous souhaitez effectuer des recherches. |
| `s={SEARCH_TERM}` | *(Facultatif)* Où {SEARCH_TERM} contient une requête conforme à l’implémentation Microsoft de la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Si aucun terme de recherche n’est spécifié, tous les enregistrements associés à `schema.name` seront renvoyés. Vous trouverez une explication plus détaillée dans l&#39;[annexe](#appendix) de ce document. |
| `entityId={ENTITY_ID}` | *(Facultatif)* Limite votre recherche à dans le dossier désigné, spécifié avec {ENTITY_ID}. |
| `limit={LIMIT}` | *(Facultatif)* Où {LIMIT} représente le nombre de résultats de recherche à renvoyer. La valeur par défaut est 50. |
| `page={PAGE}` | *(Facultatif)* Où {PAGE} représente le numéro de page utilisé pour paginer les résultats de la requête recherchée. Veuillez noter que le numéro de page commence à **0**. |


**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les résultats correspondant à la requête de recherche.

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

### Obtention d’informations structurelles sur un objet de recherche

Ce point de terminaison de recherche peut être utilisé pour obtenir les informations structurelles sur l’objet de recherche demandé.

**Format d’API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Paramètres | Description |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoire)** Où {SCHEMA} contient la valeur de classe de schéma associée aux objets de recherche. Actuellement, seul `_xdm.context.segmentdefinition` est pris en charge. |
| `namespace={NAMESPACE}` | **(Obligatoire)** Où {NAMESPACE} contient l’espace de noms dans lequel vous souhaitez effectuer des recherches. |
| `entityId={ENTITY_ID}` | **(Obligatoire)** ID de l’objet de recherche dont vous souhaitez obtenir les informations structurelles, spécifié avec {ENTITY_ID}. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations structurelles détaillées sur l’objet de recherche demandé.

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

Après avoir lu ce guide, vous comprenez mieux le fonctionnement de la recherche de segments.

## Annexe {#appendix}

Les sections suivantes apportent des informations supplémentaires sur le fonctionnement des termes de recherche. Les requêtes de recherche sont écrites de la manière suivante : `s={FieldName}:{SearchExpression}`. Par exemple, pour rechercher une définition de segment nommée AAM ou [!DNL Platform], vous utiliserez la requête de recherche suivante : `s=segmentName:AAM%20OR%20Platform`.

>  Pour connaître les bonnes pratiques, l’expression de recherche doit être codée en HTML, comme dans l’exemple ci-dessus.

### Champs de recherche {#search-fields}

Le tableau suivant répertorie les champs pouvant faire l’objet d’une recherche dans le paramètre de requête de recherche.

| Nom du champ | Description |
| ---------- | ----------- |
| folderId | Le ou les dossiers portant l’ID de dossier de votre recherche spécifiée. |
| folderLocation | Emplacement ou emplacements disposant de l’emplacement du dossier de votre recherche spécifiée. |
| parentFolderId | La définition de segment ou le dossier contenant l’identifiant du dossier parent de votre recherche spécifiée. |
| segmentId | La définition de segment qui correspond à l’identifiant du segment de votre recherche spécifiée. |
| segmentName | La définition de segment qui correspond au nom du segment de votre recherche spécifiée. |
| segmentDescription | La définition de segment qui correspond à la description du segment de votre recherche spécifiée. |

### Expression de recherche {#search-expression}

Le tableau suivant répertorie les détails du fonctionnement des requêtes de recherche lors de l’utilisation de l’API de recherche de segments.

>  Pour plus de clarté, les exemples suivants sont affichés dans un format codé non HTML. Pour connaître les bonnes pratiques, HTML de coder votre expression de recherche.

| Exemple d’expression de recherche | Description |
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

Pour obtenir une documentation plus détaillée sur la syntaxe des requêtes, veuillez lire la [documentation sur la syntaxe Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax).
