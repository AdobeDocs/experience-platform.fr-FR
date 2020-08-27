---
keywords: Experience Platform;home;popular topics;ETL;etl;etl integrations;ETL integrations
solution: Experience Platform
title: Création d’intégrations ETL
topic: overview
description: Le guide d’intégration ETL décrit les étapes générales de la création de connecteurs sécurisés et haute performance pour Experience Platform et l’ingestion de données dans Platform.
translation-type: tm+mt
source-git-commit: f4a4e65a087313dc4e2414f999e021e3f6e17137
workflow-type: tm+mt
source-wordcount: '4173'
ht-degree: 75%

---


# Développement d’intégrations ETL pour Adobe Experience Platform

The ETL integration guide outlines general steps for creating high-performance, secure connectors for [!DNL Experience Platform] and ingesting data into [!DNL Platform].


- [[ !Catalogue DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [[ ! Accès aux données DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [[ !Ingestion des données DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [API Authentication et Authorization](../tutorials/authentication.md)
- [[ ! Registre de Schéma DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

This guide also includes sample API calls to use when designing an ETL connector, with links to documentation that outlines each [!DNL Experience Platform] service, and use of its API, in more detail.

A sample integration is available on [!DNL GitHub] via the [ETL Ecosystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) under the [!DNL Apache] License Version 2.0.

## Workflow

Le diagramme de workflow suivant présente de manière générale l’intégration des composants d’Adobe Experience Platform à l’aide d’une application et d’un connecteur ETL.

![](images/etl.png)

## Composants d’Adobe Experience Platform

Plusieurs composants d’Experience Platform sont impliqués dans les intégrations de connecteur ETL. La liste suivante détaille plusieurs des composants et fonctionnalités principales :

- **Adobe Identity Management System (IMS)** — Fournit une structure d’authentification pour les services Adobe.
- **Organisation IMS** — Personne morale pouvant posséder ou accorder une licence pour des produits et des services et en permettre l’accès à ses membres.
- **Utilisateur IMS** — Membres d’une organisation IMS. La relation Organisation-utilisateur est une relation many to many.
- **[!DNL Sandbox]** - Une partition virtuelle une [!DNL Platform] instance unique, pour aider à développer et développer des applications d&#39;expérience numérique.
- **Découverte de données** — Enregistre les métadonnées des données ingérées et transformées dans [!DNL Experience Platform].
- **[!DNL Data Access]** - Fournit aux utilisateurs une interface pour accéder à leurs données dans [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Pousse les données à [!DNL Experience Platform] l&#39;aide [!DNL Data Ingestion] des API.
- **[!DNL Schema Registry]** - Définit et stocke le schéma qui décrit la structure des données à utiliser dans [!DNL Experience Platform].

## Getting started with [!DNL Experience Platform] APIs

The following sections provide additional information that you will need to know or have on-hand in order to successfully make calls to [!DNL Experience Platform] APIs.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Flux utilisateur général

To begin, an ETL user logs into the [!DNL Experience Platform] user interface (UI) and creates datasets for ingestion using a standard connector or push-service connector.

Dans l’interface utilisateur, l’utilisateur crée le jeu de données de sortie en sélectionnant un schéma de jeu de données. Le choix du schéma dépend du type de données (enregistrement ou série temporelle) ingérées dans [!DNL Platform]. En cliquant sur l’onglet Schémas de l’interface utilisateur, l’utilisateur pourra visualiser tous les schémas disponibles, ainsi que le type de comportement pris en charge par le schéma.

Dans l’outil ETL, l’utilisateur commencera à concevoir ses transformations de mappage après avoir configuré la connexion adéquate (à l’aide de ses informations d’identification). The ETL tool is assumed to already have [!DNL Experience Platform] connectors installed (process not defined in this Integration Guide).

Des maquelles pour un échantillon d’outil ETL et de workflow ont été fournis dans le [workflow ETL](./workflow.md). Bien que le format des outils ETL soit différent, la plupart d’entre eux présentent des fonctionnalités similaires.

>[!NOTE]
>
>Le connecteur ETL doit spécifier un filtre d’horodatage déterminant la date d’ingestion des données et le décalage (c.-à-d. la fenêtre pour laquelle les données doivent être lues). L’outil ETL devrait prendre en charge ces deux paramètres dans cette interface utilisateur ou dans une autre interface utilisateur pertinente. Dans Adobe Experience Platform, ces paramètres seront mappés aux dates disponibles (le cas échéant) ou à la date capturée présente dans l’objet de lot du jeu de données.

### Visualisation de la liste des jeux de données

Using the source of data for mapping, a list of all available datasets can be fetched using the [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Vous pouvez émettre une seule requête API pour visualiser tous les jeux de données disponibles (p. ex. `GET /dataSets`), la meilleure méthode étant d’inclure des paramètres de requête qui limitent la taille de la réponse.

Dans les cas où des informations _complètes_ sur les jeux de données sont demandées, le payload de la réponse peut dépasser 3 Go, ce qui est susceptible de ralentir les performances globales. Therefore, using query parameters to filter only the information needed will make [!DNL Catalog] queries more efficient.

#### Filtrage de liste

En filtrant les réponses, vous pouvez utiliser plusieurs filtres dans un seul appel en séparant les paramètres par une esperluette (`&`). Certains paramètres de requête acceptent des listes de valeurs séparées par des virgules, comme le filtre « propriétés » dans l’échantillon de requête ci-dessous.

[!DNL Catalog] les réponses sont automatiquement mesurées en fonction des limites configurées, mais le paramètre de requête &quot;limite&quot; peut être utilisé pour personnaliser les contraintes et limiter le nombre d’objets renvoyés. The pre-configured [!DNL Catalog] response limits are:

- Si aucun paramètre de limite n’est spécifié, le nombre maximal d’objets par payload de réponse est de 20.
- The global limit for all other [!DNL Catalog] queries is 100 objects.
- Pour les requêtes des jeux de données, si la variable observableSchema est demandée en utilisant le paramètre de propriétés de requête, le nombre maximal de jeux de données renvoyés est de 20.
- Les paramètres de limite non valides (y compris `limit=0`) entraîneront une erreur HTTP 400 qui décrit les plages correctes.
- Si des limites ou des décalages sont transmis en tant que paramètres de requête, ils sont prioritaires sur ceux transmis en tant qu’en-têtes.

Les paramètres de requête sont détaillés dans la [présentation du service de catalogue](../catalog/home.md).

**Format d’API**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Please refer to the [Catalog Service overview](../catalog/home.md) for detailed examples of how to make calls to the [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**Réponse**

La réponse comprend trois (`limit=3`) jeux de données indiquant le « name » (nom), la « description » et la « schemaRef » (référence schéma) comme précisés par le paramètre de requête `properties`.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Visualisation du schéma du jeu de données

La propriété « schemaRef » d’un jeu de données contient un URI faisant référence au XDM sur lequel le jeu de données est basé. Le schéma XDM (« schemaRef ») représente tous les champs _potentiels_ pouvant être utilisés par le jeu de données, mais pas nécessairement les champs _effectivement_ utilisés (voir « observableSchema » ci-dessous).

Le schéma XDM est le schéma que vous utilisez lorsque vous devez présenter à l’utilisateur une liste de tous les champs disponibles sur lesquels il est possible d’écrire.

The first &quot;schemaRef.id&quot; value in the previous response object (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) is a URI that points to a specific XDM schema in the [!DNL Schema Registry]. The schema can be retrieved by making a lookup (GET) request to the [!DNL Schema Registry] API.

>[!NOTE]
>
>La propriété « schemaRef » remplace la propriété « schema » désormais obsolète. Si « schemaRef » est absent du jeu de données ou ne contient aucune valeur, vous devrez vérifier la présence d’une propriété « schema ». Pour ce faire, remplacez « schemaRef » par « schema » dans le paramètre de requête `properties` de l’appel précédent. Pour plus d’informations sur la propriété « schema », consultez la section [Propriété « schema » du jeu de données](#dataset-schema-property-deprecated---eol-2019-05-30) ci-dessous.

**Format d’API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Requête**

La requête utilise l’URI `id` encodé URL (la valeur de l’attribut « schemaRef.id ») et requiert un en-tête Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Le format de réponse dépend du type d’en-tête Accept envoyé dans la requête. Les requêtes de recherche nécessitent également la présence d’une `version` incluse dans l’en-tête Accept. Le tableau suivant présente les en-têtes Accept disponibles pour les recherches :

| Accept | Description |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Requêtes de liste (GET), titres, identifiants et versions |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs et allOf résolus, contient des titres et des descriptions |
| `application/vnd.adobe.xed+json; version={major version}` | Brut avec $ref et allOf, contient des titres et des descriptions |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Brut avec $ref et allOf, ne contient aucun titre ni aucune description |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs et allOf résolus, ne contient aucun titre ni aucune description |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs et allOf résolus, contient des descripteurs |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` et `application/vnd.adobe.xed-full+json; version={major version}` sont les en-têtes Accept les plus fréquemment utilisés. `application/vnd.adobe.xed-id+json` est préférable pour répertorier les ressources dans la [!DNL Schema Registry] car elle renvoie uniquement les valeurs &quot;titre&quot;, &quot;id&quot; et &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` est la meilleure option pour afficher une ressource spécifique (par son « id ») car il renvoie tous les champs (imbriqués dans « properties ») ainsi que les titres et les descriptions.

**Réponse**

Le schéma JSON renvoyé décrit la structure et les informations au niveau du champ (« type », « format », « minimum », « maximum », etc.) des données, sérialisées en tant que JSON. Si vous utilisez un format de sérialisation autre que JSON pour l’ingestion (comme Parquet ou Scala), le [guide du registre des schémas](../xdm/tutorials/create-schema-api.md) comporte un tableau affichant le type JSON souhaité (« meta:xdmType ») et sa représentation correspondante dans d’autres formats.

Along with this table, the [!DNL Schema Registry] Developer Guide contains in-depth examples of all possible calls that can be made using the [!DNL Schema Registry] API.

### Propriété « schema » de jeu de données (OBSOLÈTE - FIN DE VIE 2019-05-30)

Les jeux de données peuvent contenir une propriété « schema » désormais obsolète mais qui reste temporairement disponible pour des raisons de rétrocompatibilité. Par exemple, une requête de liste (GET) similaire à celle effectuée précédemment, où « schema » a été remplacé par « schemaRef » dans le paramètre de requête `properties`, peut renvoyer ce qui suit :

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

If the &quot;schema&quot; property of a dataset is populated, this signals that the schema is a deprecated `/xdms` schema and, where supported, the ETL connector should use the value in the &quot;schema&quot; property with the `/xdms` endpoint (a deprecated endpoint in the [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) to retrieve the legacy schema.

**Format d’API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Un paramètre de requête facultatif, `expansion=xdm`, demande à l’API de développer complètement sur une seule ligne tous les schémas référencés. Cela peut être utile lorsqu’une liste de tous les champs potentiels est proposée à l’utilisateur.

**Réponse**

Tout comme les étapes de la [visualisation du schéma du jeu de données](#view-dataset-schema), la réponse contient un schéma JSON qui décrit la structure et les informations au niveau du champ des données, sérialisées en tant que JSON.

>[!NOTE]
>
>Lorsque le champ « schema » est vide ou absent, le connecteur devrait lire le champ « schemaRef » et utiliser l’[API Schema Registry](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) comme illustré dans les étapes précédentes pour [visualiser un schéma de jeu de données](#view-dataset-schema).

### La propriété « observableSchema »

La propriété « observableSchema » d’un jeu de données possède une structure JSON correspondant à celle (JSON) du schéma XDM. « observableSchema » contient les champs déjà présents dans les fichiers d’entrée ajoutés. When writing data to [!DNL Experience Platform], a user is not required to use every field from the target schema. Il devrait uniquement renseigner les champs utilisés.

Le schéma observable est le schéma que vous utiliseriez pour la lecture des données ou la présentation d’une liste des champs disponibles pour lecture/mappage.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Aperçu des données

L’application ETL peut fournir un aperçu des données ([« Figure n° 8 » dans le workflow ETL](./workflow.md)). L’API d’accès aux données propose plusieurs options de prévisualisation des données.

Vous trouverez des informations supplémentaires, notamment des instructions détaillées pour prévisualiser les données à l’aide de l’API d’accès aux données, dans le tutoriel portant sur l’[accès aux données](../data-access/tutorials/dataset-data.md).

### Obtention des détails d’un jeu de données à l’aide du paramètre de requête « properties »

Comme illustré dans les étapes ci-dessus pour [visualiser une liste de jeux de données](#view-list-of-datasets), vous pouvez demander des « files » à l’aide du paramètre de requête « properties ».

Pour plus d’informations sur l’interrogation des jeux de données et les filtres de réponse disponibles, reportez-vous à la [présentation du service de catalogue](../catalog/home.md).

**Format d’API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Réponse**

La réponse comprend un jeu de données (`limit=1`) présentant la propriété « files ».

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Liste des fichiers de jeu de données à l’aide de l’attribut « files »

Vous pouvez également utiliser une requête GET pour récupérer les détails d’un fichier à l’aide de l’attribut « files ».

**Format d’API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Réponse**

La réponse inclut l’identifiant de fichier de jeu de données comme propriété de niveau supérieur, avec les détails du fichier contenus dans l’objet d’identification du fichier de jeu de données.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Récupération des détails du fichier

The dataset file IDs returned in the previous response can be used in a GET request to fetch further file details via the [!DNL Data Access] API.

The [data access overview](../data-access/home.md) contains details on how to use the [!DNL Data Access] API.

**Format d’API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Réponse**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Aperçu des données de fichier

The &quot;href&quot; property can be used to fetch preview data via the [[!DNL Data Access API]](../data-access/home.md).

**Format d’API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

La réponse à la requête ci-dessus contient un aperçu du contenu du fichier.

More information on the [!DNL Data Access] API, including detailed requests and responses, is available in the [data access overview](../data-access/home.md).

### Obtention de « fileDescription » du jeu de données

Le composant de destination constituant la sortie des données transformées, l’ingénieur de données choisira un jeu de données de sortie ([« Figure n° 12 » dans le workflow ETL](workflow.md)). Le schéma XDM est associé au jeu de données de sortie. Les données à écrire seront identifiées par l’attribut « fileDescription » de l’entité de jeu de données des API Data Discovery. Ces informations peuvent être récupérées à l’aide d’un identifiant de jeu de données (`{DATASET_ID}`). La propriété « fileDescription » de la réponse JSON fournira les informations demandées.

**Format d’API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{DATASET_ID}` | La valeur `id` du jeu de données auquel vous tentez d’accéder. |

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Réponse**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Data will be written to [!DNL Experience Platform] using [Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).  L’écriture des données est un processus asynchrone. Lorsque des données sont écrites dans Adobe Experience Platform, un lot est créé et marqué comme réussi uniquement après que les données ont été entièrement écrites.

Data in [!DNL Experience Platform] should be written in the form of parquet files.

## Phase d’exécution

As the execution starts, the connector (as defined in the source component) will read the data from [!DNL Experience Platform] using the [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). Le processus de transformation lira les données pour une certaine période. En interne, il interrogera des lots de jeux de données source. Lors de l’interrogation, il utilisera une date de début paramétrée (qui varie pour les données de série temporelle ou les données incrémentielles) et établira une liste des fichiers de jeu de données pour ces lots. Il commencera également à demander des données pour ces fichiers de jeu de données.

### Exemples de transformations

Le document d’[échantillon de transformations ETL](./transformations.md) contient un certain nombre d’exemples de transformations, notamment la gestion des identités et les mappages de type de données. Utilisez ces transformations à titre de référence.

### Lire les données de [!DNL Experience Platform]

Using the [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), you can fetch all batches between a specified start time and end time, and sort them by the order they were created.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Details on filtering batches can be found in the [Data Access tutorial](../data-access/tutorials/dataset-data.md).

### Extraction de fichiers d’un lot

Once you have the ID for the batch you are looking for (`{BATCH_ID}`), it is possible to retrieve a list of files belonging to a specific batch via the [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).  Details for doing so are available in the [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Accès aux fichiers à l’aide de l’identifiant de fichier

Using the unique ID of a file (`{FILE_ID`), the [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) can be used to access the specific details of the file, including its name, size in bytes, and a link to download it.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

La réponse peut pointer vers un seul fichier ou vers un répertoire. Details on each can be found in the [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Accès au contenu du fichier

The [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) can be used to access the contents of a specific file. Pour récupérer le contenu, une requête GET est effectuée à l’aide de la valeur renvoyée pour `_links.self.href` lors de l’accès à un fichier à l’aide de l’identifiant de fichier.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La réponse à cette requête inclut le contenu du fichier. Pour plus d’informations, y compris des détails sur la pagination des réponses, consultez le tutoriel [Comment interroger des données via l’API d’accès aux données](../data-access/tutorials/dataset-data.md).

### Validation des enregistrements pour la conformité aux schémas

Lors de l’écriture des données, l’utilisateur peut choisir de valider les données selon les règles de validation définies dans le schéma XDM. Pour plus d’informations sur la validation des schémas, consultez l’[Ecosystem Integration Reference Code ETL sur [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

If you are using the reference implementation found on [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), you can turn on schema validation in this implementation using the system property `-DenableSchemaValidation=true`.

La validation peut être effectuée pour les types XDM logiques à l’aide d’attributs tels que `minLength` et `maxlength` pour les chaînes, `minimum` et `maximum` pour les entiers, etc. Le [guide de développement de l’API Schema Registry](../xdm/api/getting-started.md) comporte un tableau décrivant les types XDM et les propriétés qui peuvent être utilisées pour la validation.

>[!NOTE]
>
>Les valeurs minimales et maximales fournies pour divers types d’`integer` sont les valeurs MIN et MAX que le type peut prendre en charge. Vous pouvez cependant augmenter ou diminuer ces valeurs si vous le souhaitez.

### Création d’un lot

Once the data is processed, the ETL tool will write the data back to [!DNL Experience Platform] using the [Batch Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Avant de pouvoir ajouter des données à un jeu de données, celles-ci doivent être liées à un lot qui sera chargé ultérieurement dans un jeu de données spécifique.

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Vous trouverez des détails sur la création d’un lot ainsi que des échantillons de requêtes et de réponses dans la [présentation de l’ingestion par lots](../ingestion/batch-ingestion/overview.md).

### Écriture dans un jeu de données

Une fois le nouveau lot créé avec succès, les fichiers peuvent être chargés vers un jeu de données spécifique. Plusieurs fichiers peuvent être publiés dans un lot jusqu’à ce qu’il soit converti. Les fichiers peuvent être chargés à l’aide de l’_API Small File Upload_. Cependant, si vos fichiers sont trop volumineux et dépassent la limite de la passerelle, vous pouvez utiliser l’_API Large File Upload_. Vous trouverez des informations détaillées sur l’utilisation de ces deux API dans la [présentation de l’ingestion par lots](../ingestion/batch-ingestion/overview.md).

**Requête**

Data in [!DNL Experience Platform] should be written in the form of parquet files.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marquage du chargement par lots comme étant terminé

Une fois que tous les fichiers ont été chargés dans le lot, il peut être marqué comme étant terminé. By doing this, the [!DNL Catalog] &quot;DataSetFile&quot; entries are created for the completed files and associated with the generate batch. The [!DNL Catalog] batch is then marked as successful, which triggers downstream flows to ingest the available data.

Les données arriveront d’abord à l’emplacement d’évaluation sur Adobe Experience Platform, puis seront déplacées vers l’emplacement final après catalogage et validation. Les lots seront marqués comme réussis une fois toutes les données déplacées vers un emplacement permanent.

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

En cas de succès de l’opération, la réponse renvoie un état HTTP 200 OK, et le corps de la réponse est vide.

L’outil ETL veillera à noter l’horodatage du ou des jeux de données source lors de la lecture des données.

La prochaine fois que la transformation sera exécutée (probablement par planification ou par événement d’appel), l’ETL lancera la requête des données de l’horodatage précédemment enregistré et celle de toutes les données à venir.

### Obtention de l’état du dernier lot

Avant d’exécuter de nouvelles tâches dans l’outil ETL, vous devez vous assurer que le dernier lot a bien été terminé. The [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) provides a batch-specific option which provides the details of the relevant batches.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

De nouvelles tâches peuvent être planifiées si la valeur « status » du lot précédent est « success », comme illustré ci-dessous :

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Obtention de l’état du dernier lot par identifiant

An individual batch status can be retrieved through the [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) by issuing a GET request using the `{BATCH_ID}`. L’identifiant `{BATCH_ID}` utilisé est identique à celui renvoyé lors de la création du lot.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse - Réussite**

La réponse suivante indique la réussite de l’opération (« success ») :

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Réponse - Échec**

En cas d’échec, les erreurs (« errors ») peuvent être extraites de la réponse et affichées sur l’outil ETL sous forme de messages d’erreur.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Données incrémentielles / données instantanées et événements / profils

Les données peuvent être représentées dans une matrice 2 x 2 comme suit :

| Événements incrémentiels | Profils incrémentiels |
|-------------------------------|----------------------|
| Événements instantanés (plus rares) | Profils instantanés |

Les données d’événement sont généralement définies par la présence de colonnes d’horodatage indexées dans chaque ligne.

Les données de profil sont généralement définies par le fait qu’il n’existe aucun horodatage dans les données et que chaque ligne peut être identifiée par une clé primaire/composite.

Les données incrémentielles sont définies par le fait que seules des nouvelles données/des données mises à jour arrivent dans le système, en supplément des données déjà dans les jeux de données.

Les données instantanées sont définies par l’arrivée dans le système de toutes les données, qui remplacent une partie ou l’intégralité des données déjà présentes dans un jeu de données.

Dans le cas d’événements incrémentiels, l’outil ETL devrait utiliser les dates disponibles/créer la date de l’entité de lot. En cas de service Push, les dates disponibles seront absentes. L’outil utilisera donc la date de création/mise à jour du lot pour marquer les incréments. Chaque lot d’événements incrémentiels doit être traité.

Pour les profils incrémentiels, l’outil ETL utilisera les dates de création/mise à jour de l’entité de lot. En règle générale, chaque lot de données de profil incrémentiel doit être traité.

En raison de la taille des données, les événements instantanés sont beaucoup plus rares. Si cela était toutefois nécessaire, l’outil ETL ne doit sélectionner que le dernier lot à traiter.

Lors de l’utilisation des profils instantanés, l’outil ETL devra sélectionner le dernier lot de données arrivé dans le système. Si vous devez suivre les versions des modifications, tous les lots devront cependant être traités. Le traitement de la déduplication dans le processus ETL permettra de contrôler les frais de stockage.

## Relecture de lot et retraitement des données

La relecture de lot et le retraitement des données peuvent être requis dans les cas où un client découvre que, au cours des « n » derniers jours, le traitement des données par ETL ne s’est pas déroulé comme prévu ou que les données source elles-mêmes n’étaient peut-être pas exactes.

To do this, the client&#39;s data administrators will use the [!DNL Platform] UI to remove the batches containing corrupt data. Ensuite, l’ETL devra probablement être réexécuté, ce qui fournira de nouvelles données correctes. Si la source elle-même contenait des données corrompues, l’ingénieur/l’administrateur des données devra corriger les lots source et ingérer de nouveau les données (soit dans Adobe Experience Platform, soit à l’aide de connecteurs ETL).

Selon le type de données généré, l’ingénieur de données choisira de supprimer un seul lot ou tous les lots de certains jeux de données. Data will be removed/archived as per [!DNL Experience Platform] guidelines.

Il est probable que la fonctionnalité ETL de purge des données ait un rôle important.

Une fois la purge terminée, les administrateurs client devront reconfigurer Adobe Experience Platform pour redémarrer le traitement des services principaux à partir du moment de suppression des lots.

## Traitement simultané de lot

À la discrétion du client, les administrateurs/ingénieurs de données peuvent décider d’extraire, de transformer et de charger les données de manière séquentielle ou simultanée, selon les caractéristiques d’un jeu de données spécifique. Cela dépendra également de ce que le client compte faire des données transformées.

Par exemple, si le client persiste vers un magasin de persistance modifiable et que la séquence ou l’ordre des événements est important, le client peut avoir besoin de traiter rigoureusement les tâches avec des transformations ETL séquentielles.

Dans d’autres cas, les données altérées peuvent être traitées par des applications/processus en aval qui trient en interne à l’aide d’un horodatage spécifié. Dans ces cas, des transformations ETL parallèles peuvent être viables pour améliorer les temps de traitement.

Pour les lots source, cela dépendra à nouveau des préférences du client et des contraintes de la part du consommateur. Si les données source peuvent être collectées en parallèle sans tenir compte de la régence/de l’ordre d’une ligne, le processus de transformation peut alors créer des lots de traitement avec un degré de parallélisme plus élevé (optimisation basée sur le traitement altéré). Si la transformation doit respecter les horodatages ou modifier l’ordre de priorité, l’API d’accès aux données ou le planificateur/l’appel d’outil ETL devra toutefois s’assurer que les lots sont traités dans l’ordre lorsque cela est possible.

## Report

Le report est un processus au cours duquel les données d’entrée ne sont pas encore suffisamment complètes pour être envoyées aux processus en aval, mais peuvent être utilisées ultérieurement. Les clients détermineront leur propre tolérance en ce qui concerne le fenêtrage des données pour la future mise en correspondance par rapport au coût du traitement. Cela permettra d’éclairer leur décision de mettre de côté les données et de les retraiter lors de la prochaine exécution de la transformation, dans l’espoir qu’elles pourront être enrichies et réconciliées/assemblées ultérieurement dans la fenêtre de rétention. Ce cycle se poursuit jusqu’à ce que la ligne soit suffisamment traitée ou qu’elle soit considérée comme obsolète et que tout investissement soit jugé inutile. Chaque itération générera des données différées qui constituent un sur-ensemble de toutes les données différées des itérations précédentes.

Adobe Experience Platform does not identify deferred data currently, so client implementations must rely on the ETL and Dataset manual configurations to create another dataset in [!DNL Platform] mirroring the source dataset which can be used to keep deferred data. Dans ce cas, les données différées sont similaires aux données instantanées. Dans chaque exécution de la transformation ETL, les données source sont combinées aux données différées et envoyées pour traitement.

## Journal des modifications

| Date | Action | Description |
| ---- | ------ | ----------- |
| 19/01/2019 | Suppression de la propriété « fields » des jeux de données | Les jeux de données comprenaient auparavant une propriété « fields » qui contenait une copie du schéma. Cette fonctionnalité ne doit plus être utilisée. Si la propriété « fields » est trouvée, elle doit être ignorée et la propriété « observedSchema » ou « schemaRef » utilisée à la place. |
| 15/03/2019 | Ajout de la propriété « schemaRef » aux jeux de données | La propriété « schemaRef » d’un jeu de données contient un URI référençant le XDM sur lequel le jeu de données est basé et représente tous les champs potentiels pouvant être utilisés par le jeu de données. |
| 15/03/2019 | Tous les identifiants d’utilisateur final mappent vers la propriété « identityMap ». | « identityMap » contient tous les identifiants uniques d’un sujet, tels que l’identifiant de logiciel de gestion de la relation client, l’ECID ou l’identifiant du programme de fidélité. This map is used by [[!DNL Identity Service]](../identity-service/home.md) to resolve all known and anonymous identities of a subject, forming a single identity graph for each end-user. |
| 30/05/2019 | Fin de vie et suppression de la propriété « schema » des jeux de données | La propriété « schema » du jeu de données fournissait un lien de référence vers le schéma à l’aide du point de terminaison `/xdms` obsolète dans l’API [!DNL Catalog] This has been replaced by a &quot;schemaRef&quot; that provides the &quot;id&quot;, &quot;version&quot;, and &quot;contentType&quot; of the schema as referenced in the new [!DNL Schema Registry] API. |