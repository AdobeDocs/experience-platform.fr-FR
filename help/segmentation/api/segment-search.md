---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;
solution: Adobe Experience Platform
title: Guide du développeur d’API de segmentation
topic: guide
translation-type: tm+mt
source-git-commit: f489e9f9dfc9c7e94f76a6825e7ca24c41ee8a66
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 2%

---


# Recherche de segment

La recherche de segments permet de rechercher et d’indexer des champs configurables contenus dans diverses sources de données et de les renvoyer en temps quasi réel.

Ce guide fournit des informations qui vous aideront à mieux comprendre la recherche de segments et inclut des exemples d’appels d’API pour exécuter des actions de base à l’aide de l’API.

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API de segmentation. Avant de continuer, consultez le guide [du développeur de](getting-started.md)segmentation.

En particulier, la section [Prise en main de la](getting-started.md) sectiondu guide du développeur de segmentation contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à l’API de plateforme d’expérience.

Outre les en-têtes requis décrits dans la section Prise en main, toutes les requêtes de l’API de recherche de segment nécessitent l’en-tête supplémentaire suivant :

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
| `s={SEARCH_TERM}` | *(Facultatif)* Où {SEARCH_TERM} représente une requête conforme à l&#39;implémentation par Microsoft de la syntaxe [de recherche de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si aucun terme de recherche n&#39;est spécifié, tous les enregistrements associés `schema.name` seront renvoyés. On trouvera une explication plus détaillée dans l&#39; [annexe](#appendix) du présent document. |

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

Une réponse réussie renvoie l’état HTTP 200 avec les informations suivantes.

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
| `s={SEARCH_TERM}` | *(Facultatif)* Où {SEARCH_TERM} contient une requête conforme à l&#39;implémentation par Microsoft de la syntaxe [de recherche de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si aucun terme de recherche n&#39;est spécifié, tous les enregistrements associés `schema.name` seront renvoyés. On trouvera une explication plus détaillée dans l&#39; [annexe](#appendix) du présent document. |
| `entityId={ENTITY_ID}` | *(Facultatif)* Limite votre recherche au dossier désigné, spécifié avec {ENTITY_ID}. |
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

Après avoir lu ce guide, vous comprenez mieux comment fonctionne la recherche de segments. Pour plus d’informations sur la segmentation, consultez la présentation [de la](../home.md)segmentation.

## Annexe {#appendix}

Les sections suivantes fournissent des informations supplémentaires sur le fonctionnement des termes de recherche. Les requêtes de recherche sont rédigées de la manière suivante : `s={FieldName}:{SearchExpression}`. Ainsi, par exemple, pour rechercher un segment nommé AAM ou Platform, vous utiliseriez la requête de recherche suivante : `s=segmentName:AAM%20OR%20Platform`.

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

### expression de recherche {#search-expression}

Le tableau suivant liste les détails du fonctionnement des requêtes de recherche lors de l&#39;utilisation de l&#39;API de recherche de segment.

>!![NOTE] Les exemples suivants sont présentés dans un format non codé en HTML pour une meilleure clarté. Pour les meilleures pratiques, code HTML pour votre expression de recherche.

| Exemple d&#39;expression de recherche | Description |
| ------------------------- | ----------- |
| foo | Recherchez n&#39;importe quel mot. Cela renverra des résultats si le mot &quot;foo&quot; se trouve dans l’un des champs recherchés. |
| foo AND bar | Recherche booléenne. Cela retournera des résultats si **** les mots &quot;foo&quot; et &quot;bar&quot; se trouvent dans l’un des champs recherchés. |
| barre d’état OU | Recherche booléenne. Cela retournera des résultats si **** le mot &quot;foo&quot; ou le mot &quot;bar&quot; se trouvent dans l’un des champs disponibles pour la recherche. |
| barre FOI NOT | Recherche booléenne. Cela retournera des résultats si le mot &quot;foo&quot; est trouvé mais que le mot &quot;bar&quot; ne se trouve dans aucun des champs recherchés. |
| name: foo AND bar | Recherche booléenne. Cela retournera des résultats si **les deux** mots &quot;foo&quot; et &quot;bar&quot; se trouvent dans le champ &quot;name&quot;. |
| run* | Recherche de caractères génériques. L’utilisation d’un astérisque (*) correspond à 0 caractère ou plus, ce qui signifie qu’il renvoie des résultats si le contenu de l’un des champs recherchés contient un mot qui début avec &quot;run&quot;. Par exemple, les résultats seront renvoyés si les mots &quot;run&quot;, &quot;running&quot;, &quot;runner&quot; ou &quot;runt&quot; apparaissent. |
| cam ? | Recherche de caractères génériques. Utilisation d’un point d’interrogation (?) ne correspond qu’à un seul caractère, ce qui signifie qu’il renvoie des résultats si le contenu de l’un des champs recherchés est début avec &quot;cam&quot; et une lettre supplémentaire. Par exemple, les résultats seront renvoyés si les mots &quot;camp&quot; ou &quot;cams&quot; apparaissent, mais pas si les mots &quot;caméra&quot; ou &quot;feu de camp&quot; apparaissent. |
| &quot;parapluie bleu&quot; | Recherche d&#39;expression. Cela retournera des résultats si le contenu de l&#39;un des champs recherchés contient l&#39;expression complète &quot;parapluie bleu&quot;. |
| bleu\~ | Une recherche floue. Vous pouvez éventuellement placer un nombre compris entre 0 et 2 après le tilde (~) pour spécifier la distance de modification. Par exemple, &quot;blue\~1&quot; renvoie &quot;blue&quot;, &quot;blues&quot; ou &quot;colle&quot;. La recherche floue ne peut **être appliquée qu** &#39;aux termes, et non aux expressions. Cependant, vous pouvez ajouter des tildes à la fin de chaque mot d’une phrase. Par exemple, &quot;camping\~ à\~ l\~ été\~&quot; correspond à &quot;camping en été&quot;. |
| &quot;aéroport de l&#39;hôtel&quot;\~5 | Recherche de proximité. Ce type de recherche permet de rechercher des termes proches les uns des autres dans un document. Par exemple, l&#39;expression `"hotel airport"~5` trouvera les termes &quot;hôtel&quot; et &quot;aéroport&quot; à moins de 5 mots l&#39;un de l&#39;autre dans un document. |
| `/a[0-9]+b$/` | Recherche d’expressions régulière. Ce type de recherche trouve une correspondance basée sur le contenu entre les barres obliques &quot;/&quot;, comme indiqué dans la classe RegExp. Par exemple, pour rechercher des documents contenant &quot;motel&quot; ou &quot;hotel&quot;, spécifiez `/[mh]otel/`. Les recherches d’expressions régulières sont comparées à des mots simples. |

Pour obtenir une documentation plus détaillée sur la syntaxe de la requête, veuillez lire la documentation [sur la syntaxe de la requête](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene.
