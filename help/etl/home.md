---
keywords: Experience Platform;accueil;rubriques populaires;ETL;etl;intégrations etl;intégrations ETL
solution: Experience Platform
title: Développement d’intégrations ETL pour Adobe Experience Platform
description: Le guide d’intégration ETL décrit les étapes générales de la création de connecteurs sécurisés et haute performance pour Experience Platform et l’ingestion de données dans Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '3977'
ht-degree: 99%

---

# Développement d’intégrations ETL pour Adobe Experience Platform

Le guide d’intégration ETL décrit les étapes générales de la création de connecteurs sécurisés et haute performance pour [!DNL Experience Platform] et l’ingestion de données dans [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Authentification et autorisation pour les API Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Ce guide comprend également des exemples d’appels d’API à utiliser lors de la conception d’un connecteur ETL, avec des liens vers la documentation détaillant chaque service [!DNL Experience Platform] et l’utilisation de son API.

Un exemple d’intégration est disponible sur [!DNL GitHub] via l’[Ecosystem Integration Reference Code ETL](https://github.com/adobe/acp-data-services-etl-reference) sous la version 2.0 de la licence [!DNL Apache].

## Workflow

Le diagramme de workflow suivant présente de manière générale l’intégration des composants d’Adobe Experience Platform à l’aide d’une application et d’un connecteur ETL.

![](images/etl.png)

## Composants d’Adobe Experience Platform

Plusieurs composants d’Experience Platform sont impliqués dans les intégrations de connecteur ETL. La liste suivante détaille plusieurs des composants et fonctionnalités principales :

- **Adobe IDentity Management System (IMS)** — Fournit une structure d’authentification pour les services Adobe.
- **Organisation IMS** — Personne morale pouvant posséder ou accorder une licence pour des produits et des services et en permettre l’accès à ses membres.
- **Utilisateur IMS** — Membres d’une organisation IMS. La relation Organisation-utilisateur est une relation many to many.
- **[!DNL Sandbox]** - Une partition virtuelle d’une instance de [!DNL Platform] unique, qui aide au développement et à l’évolution des applications d’expérience digitale.
- **Découverte de données** — Enregistre les métadonnées des données ingérées et transformées dans [!DNL Experience Platform].
- **[!DNL Data Access]** - Fournit aux utilisateurs une interface pour accéder à leurs données dans [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Envoie les données à [!DNL Experience Platform] avec les API [!DNL Data Ingestion].
- **[!DNL Schema Registry]** - Définit et stocke des schémas qui décrivent la structure des données à utiliser dans [!DNL Experience Platform].

## Prise en main des API [!DNL Experience Platform]

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin ou dont vous devrez disposer pour passer avec succès des appels aux API [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Flux utilisateur général

Pour commencer, un utilisateur ETL se connecte à l’interface utilisateur d’[!DNL Experience Platform] et crée des jeux de données destinés à être ingérés à l’aide d’un connecteur standard ou d’un connecteur de service Push.

Dans l’interface utilisateur, l’utilisateur crée le jeu de données de sortie en sélectionnant un schéma de jeu de données. Le choix du schéma dépend du type de données (enregistrement ou série temporelle) ingérées dans [!DNL Platform]. En cliquant sur l’onglet Schémas de l’interface utilisateur, l’utilisateur pourra visualiser tous les schémas disponibles, ainsi que le type de comportement pris en charge par le schéma.

Dans l’outil ETL, l’utilisateur commencera à concevoir ses transformations de mappage après avoir configuré la connexion adéquate (à l’aide de ses informations d’identification). L’outil ETL est supposé déjà disposer de connecteurs [!DNL Experience Platform] installés (ce processus n’est pas défini dans ce guide d’intégration).

Des maquelles pour un échantillon d’outil ETL et de workflow ont été fournis dans le [workflow ETL](./workflow.md). Bien que le format des outils ETL soit différent, la plupart d’entre eux présentent des fonctionnalités similaires.

>[!NOTE]
>
>Le connecteur ETL doit spécifier un filtre d’horodatage déterminant la date d’ingestion des données et le décalage (c.-à-d. la fenêtre pour laquelle les données doivent être lues). L’outil ETL devrait prendre en charge ces deux paramètres dans cette interface utilisateur ou dans une autre interface utilisateur pertinente. Dans Adobe Experience Platform, ces paramètres seront mappés aux dates disponibles (le cas échéant) ou à la date capturée présente dans l’objet de lot du jeu de données.

### Visualisation de la liste des jeux de données

En utilisant la source des données pour le mappage, une liste de tous les jeux de données disponibles peut être récupérée à l’aide de l’[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Vous pouvez émettre une seule requête API pour visualiser tous les jeux de données disponibles (p. ex. `GET /dataSets`), la meilleure méthode étant d’inclure des paramètres de requête qui limitent la taille de la réponse.

Dans les cas où des informations complètes sur les jeux de données sont demandées, le payload de la réponse peut dépasser 3 Go, ce qui est susceptible de ralentir les performances globales. Par conséquent, l’utilisation de paramètres de requête pour filtrer uniquement les informations nécessaires rendra les requêtes du [!DNL Catalog] plus efficaces.

#### Filtrage de liste

En filtrant les réponses, vous pouvez utiliser plusieurs filtres dans un seul appel en séparant les paramètres par une esperluette (`&`). Certains paramètres de requête acceptent des listes de valeurs séparées par des virgules, comme le filtre « propriétés » dans l’échantillon de requête ci-dessous.

Les réponses du [!DNL Catalog] sont automatiquement limitées en fonction des limites configurées. Le paramètre de requête « limite » peut cependant être utilisé pour personnaliser les contraintes et limiter le nombre d’objets renvoyés. Voici les limites de réponse préconfigurées du [!DNL Catalog] :

- Si aucun paramètre de limite n’est spécifié, le nombre maximal d’objets par payload de réponse est de 20.
- La limite globale pour toutes les autres requêtes de [!DNL Catalog] est de 100 objets.
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consultez la [présentation du service de catalogue](../catalog/home.md) pour obtenir des exemples détaillés sur la manière d’effectuer des appels vers l’[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

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

La propriété « schemaRef » d’un jeu de données contient un URI faisant référence au XDM sur lequel le jeu de données est basé. Le schéma XDM (« schemaRef ») représente tous les champs potentiels pouvant être utilisés par le jeu de données, mais pas nécessairement les champs effectivement utilisés (voir « observableSchema » ci-dessous).

Le schéma XDM est le schéma que vous utilisez lorsque vous devez présenter à l’utilisateur une liste de tous les champs disponibles sur lesquels il est possible d’écrire.

La première valeur « schemaRef.id » dans l’objet de réponse précédent (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) est un URI qui pointe vers un schéma XDM spécifique dans le [!DNL Schema Registry]. Le schéma peut être récupéré en envoyant une requête de recherche (GET) à l’API [!DNL Schema Registry].

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>`application/vnd.adobe.xed-id+json` et `application/vnd.adobe.xed-full+json; version={major version}` sont les en-têtes Accept les plus fréquemment utilisés. `application/vnd.adobe.xed-id+json` est la meilleure option pour répertorier les ressources dans le [!DNL Schema Registry], car il renvoie uniquement les valeurs « titre », « id » et « version ». `application/vnd.adobe.xed-full+json; version={major version}` est la meilleure option pour afficher une ressource spécifique (par son « id ») car il renvoie tous les champs (imbriqués dans « properties ») ainsi que les titres et les descriptions.

**Réponse**

Le schéma JSON renvoyé décrit la structure et les informations au niveau du champ (« type », « format », « minimum », « maximum », etc.) des données, sérialisées en tant que JSON. Si vous utilisez un format de sérialisation autre que JSON pour l’ingestion (comme Parquet ou Scala), le [guide du registre des schémas](../xdm/tutorials/create-schema-api.md) comporte un tableau affichant le type JSON souhaité (« meta:xdmType ») et sa représentation correspondante dans d’autres formats.

Outre ce tableau, le guide de développement du [!DNL Schema Registry] contient des exemples détaillés de tous les appels possibles à l’aide de l’API [!DNL Schema Registry].

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

Si la propriété « schema » d’un jeu de données est renseignée, cela indique que le schéma est un schéma `/xdms` obsolète. C’est pourquoi, lorsqu’il est pris en charge, le connecteur ETL devrait utiliser la valeur de la propriété « schema » avec le point d’entrée `/xdms` (un point d’entrée obsolète de l’[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) pour récupérer l’ancien schéma.

**Format d’API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
>Lorsque le champ « schema » est vide ou absent, le connecteur devrait lire le champ « schemaRef » et utiliser l’[API Schema Registry](https://www.adobe.io/experience-platform-apis/references/schema-registry/) comme illustré dans les étapes précédentes pour [visualiser un schéma de jeu de données](#view-dataset-schema).

### La propriété « observableSchema »

La propriété « observableSchema » d’un jeu de données possède une structure JSON correspondant à celle (JSON) du schéma XDM. « observableSchema » contient les champs déjà présents dans les fichiers d’entrée ajoutés. Lorsqu’il écrit des données dans [!DNL Experience Platform], l’utilisateur n’est pas tenu de se servir de tous les champs du schéma cible. Il devrait uniquement renseigner les champs utilisés.

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Réponse**

La réponse comprend un jeu de données (`limit=1`) présentant la propriété « files ».

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSetFiles?dataSetId=5bf479a6a8c862000050e3c7"
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

La réponse inclut l’identifiant de fichier de jeu de données comme propriété de niveau supérieur, avec les détails du fichier contenus dans l’objet d’identification du fichier de jeu de données.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

Les identifiants du fichier de jeu de données renvoyés dans la réponse précédente peuvent être utilisés dans une requête GET pour récupérer d’autres détails de fichier via l’API d’[!DNL Data Access].

La [présentation de l’accès aux données](../data-access/home.md) contient des détails sur l’utilisation de l’API [!DNL Data Access].

**Format d’API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

La propriété « href » peut être utilisée pour récupérer des données de prévisualisation via l’API d’[[!DNL Data Access API]](../data-access/home.md).

**Format d’API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

La réponse à la requête ci-dessus contient un aperçu du contenu du fichier.

Vous trouverez plus d’informations sur l’API d’[!DNL Data Access], y compris des requêtes et des réponses détaillées, dans la [présentation de l’accès aux données](../data-access/home.md).

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
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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

Les données seront écrites dans [!DNL Experience Platform] à l’aide de l’[API Batch Ingestion](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  L’écriture des données est un processus asynchrone. Lorsque des données sont écrites dans Adobe Experience Platform, un lot est créé et marqué comme réussi uniquement après que les données ont été entièrement écrites.

Dans [!DNL Experience Platform], les données devraient être écrites sous la forme de fichiers parquet.

## Phase d’exécution

Lorsque l’exécution démarre, le connecteur (tel que défini dans le composant source) lit les données d’[!DNL Experience Platform] à l’aide de l’[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). Le processus de transformation lira les données pour une certaine période. En interne, il interrogera des lots de jeux de données source. Lors de l’interrogation, il utilisera une date de début paramétrée (qui varie pour les données de série temporelle ou les données incrémentielles) et établira une liste des fichiers de jeu de données pour ces lots. Il commencera également à demander des données pour ces fichiers de jeu de données.

### Exemples de transformations

Le document d’[échantillon de transformations ETL](./transformations.md) contient un certain nombre d’exemples de transformations, notamment la gestion des identités et les mappages de type de données. Utilisez ces transformations à titre de référence.

### Lecture des données à partir d’[!DNL Experience Platform]

À l’aide de l’[[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), vous pouvez récupérer tous les lots entre une heure de début et une heure de fin spécifiques, puis les trier selon l’ordre dans lequel ils ont été créés.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Vous trouverez des détails sur le filtrage des lots dans le [tutoriel portant sur l’accès aux données](../data-access/tutorials/dataset-data.md).

### Extraction de fichiers d’un lot

Une fois que vous disposez de l’identifiant du lot que vous recherchez (`{BATCH_ID}`), il est possible de récupérer une liste de fichiers appartenant à un lot en particulier via l’[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Pour plus d’informations sur ce processus, reportez-vous au tutoriel portant sur l’[[!DNL Data Access] ](../data-access/tutorials/dataset-data.md).

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Accès aux fichiers à l’aide de l’identifiant de fichier

À l’aide de l’ID unique d’un fichier (`{FILE_ID`), le [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) permet d’accéder aux détails spécifiques du fichier, notamment son nom, sa taille en octets et un lien pour le télécharger.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La réponse peut pointer vers un seul fichier ou vers un répertoire. Vous trouverez des informations détaillées sur chaque option dans le tutoriel portant sur l’[[!DNL Data Access] ](../data-access/tutorials/dataset-data.md).

### Accès au contenu du fichier

Le [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) permet d’accéder au contenu d’un fichier spécifique. Pour récupérer le contenu, une requête GET est effectuée à l’aide de la valeur renvoyée pour `_links.self.href` lors de l’accès à un fichier à l’aide de l’identifiant de fichier.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La réponse à cette requête inclut le contenu du fichier. Pour plus d’informations, y compris des détails sur la pagination des réponses, consultez le tutoriel [Comment interroger des données via l’API d’accès aux données](../data-access/tutorials/dataset-data.md).

### Validation des enregistrements pour la conformité aux schémas

Lors de l’écriture des données, l’utilisateur peut choisir de valider les données selon les règles de validation définies dans le schéma XDM. Pour plus d’informations sur la validation des schémas, consultez l’[Ecosystem Integration Reference Code ETL sur [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Si vous utilisez l’implémentation de référence disponible sur [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), vous pouvez activer la validation des schémas dans cette implémentation à l’aide de la propriété système `-DenableSchemaValidation=true`.

La validation peut être effectuée pour les types XDM logiques à l’aide d’attributs tels que `minLength` et `maxlength` pour les chaînes, `minimum` et `maximum` pour les entiers, etc. Le [guide de développement de l’API Schema Registry](../xdm/api/getting-started.md) comporte un tableau décrivant les types XDM et les propriétés qui peuvent être utilisées pour la validation.

>[!NOTE]
>
>Les valeurs minimales et maximales fournies pour divers types d’`integer` sont les valeurs MIN et MAX que le type peut prendre en charge. Vous pouvez cependant augmenter ou diminuer ces valeurs si vous le souhaitez.

### Création d’un lot

Une fois les données traitées, l’outil ETL réécrit les données dans [!DNL Experience Platform] à l’aide de l’[API Batch Ingestion](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Avant de pouvoir ajouter des données à un jeu de données, celles-ci doivent être liées à un lot qui sera chargé ultérieurement dans un jeu de données spécifique.

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Vous trouverez des détails sur la création d’un lot ainsi que des échantillons de requêtes et de réponses dans la [présentation de l’ingestion par lots](../ingestion/batch-ingestion/overview.md).

### Écriture dans un jeu de données

Une fois le nouveau lot créé avec succès, les fichiers peuvent être chargés vers un jeu de données spécifique. Plusieurs fichiers peuvent être publiés dans un lot jusqu’à ce qu’il soit converti. Les fichiers peuvent être chargés à l’aide de l’API Small File Upload. Cependant, si vos fichiers sont trop volumineux et dépassent la limite de la passerelle, vous pouvez utiliser l’API Large File Upload. Vous trouverez des informations détaillées sur l’utilisation de ces deux API dans la [présentation de l’ingestion par lots](../ingestion/batch-ingestion/overview.md).

**Requête**

Dans [!DNL Experience Platform], les données devraient être écrites sous la forme de fichiers parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marquage du chargement par lots comme étant terminé

Une fois que tous les fichiers ont été chargés dans le lot, il peut être marqué comme étant terminé. Cette action crée les entrées « DataSetFile » du [!DNL Catalog] pour les fichiers terminés et les associe au lot généré. Le lot de [!DNL Catalog] est marqué comme réussi, ce qui déclenche les flux en aval afin d’ingérer les données disponibles.

Les données arriveront d’abord à l’emplacement d’évaluation sur Adobe Experience Platform, puis seront déplacées vers l’emplacement final après catalogage et validation. Les lots seront marqués comme réussis une fois toutes les données déplacées vers un emplacement permanent.

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

En cas de succès de l’opération, la réponse renvoie un état HTTP 200 OK, et le corps de la réponse est vide.

L’outil ETL veillera à noter l’horodatage du ou des jeux de données source lors de la lecture des données.

La prochaine fois que la transformation sera exécutée (probablement par planification ou par événement d’appel), l’ETL lancera la requête des données de l’horodatage précédemment enregistré et celle de toutes les données à venir.

### Obtention de l’état du dernier lot

Avant d’exécuter de nouvelles tâches dans l’outil ETL, vous devez vous assurer que le dernier lot a bien été terminé. Le [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) fournit une option spécifique pour les lots qui indique les détails des lots pertinents.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

De nouvelles tâches peuvent être planifiées si la valeur « status » du lot précédent est « success », comme illustré ci-dessous :

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

Un état de lot individuel peut être récupéré via l’[[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) en émettant une requête GET à l’aide du `{BATCH_ID}`. L’identifiant `{BATCH_ID}` utilisé est identique à celui renvoyé lors de la création du lot.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse - Réussite**

La réponse suivante indique la réussite de l’opération (« success ») :

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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

Pour ce faire, les administrateurs des données des clients utiliseront l’interface utilisateur de [!DNL Platform] pour supprimer les lots contenant des données corrompues. Ensuite, l’ETL devra probablement être réexécuté, ce qui fournira de nouvelles données correctes. Si la source elle-même contenait des données corrompues, l’ingénieur/l’administrateur des données devra corriger les lots source et ingérer de nouveau les données (soit dans Adobe Experience Platform, soit à l’aide de connecteurs ETL).

Selon le type de données généré, l’ingénieur de données choisira de supprimer un seul lot ou tous les lots de certains jeux de données. Les données seront supprimées/archivées conformément aux directives d’[!DNL Experience Platform].

Il est probable que la fonctionnalité ETL de purge des données ait un rôle important.

Une fois la purge terminée, les administrateurs client devront reconfigurer Adobe Experience Platform pour redémarrer le traitement des services principaux à partir du moment de suppression des lots.

## Traitement simultané de lot

À la discrétion du client, les administrateurs/ingénieurs de données peuvent décider d’extraire, de transformer et de charger les données de manière séquentielle ou simultanée, selon les caractéristiques d’un jeu de données spécifique. Cela dépendra également de ce que le client compte faire des données transformées.

Par exemple, si le client persiste vers un magasin de persistance modifiable et que la séquence ou l’ordre des événements est important, le client peut avoir besoin de traiter rigoureusement les tâches avec des transformations ETL séquentielles.

Dans d’autres cas, les données altérées peuvent être traitées par des applications/processus en aval qui trient en interne à l’aide d’un horodatage spécifié. Dans ces cas, des transformations ETL parallèles peuvent être viables pour améliorer les temps de traitement.

Pour les lots source, cela dépendra à nouveau des préférences du client et des contraintes de la part du consommateur. Si les données source peuvent être collectées en parallèle sans tenir compte de la régence/de l’ordre d’une ligne, le processus de transformation peut alors créer des lots de traitement avec un degré de parallélisme plus élevé (optimisation basée sur le traitement altéré). Si la transformation doit respecter les horodatages ou modifier l’ordre de priorité, l’API d’accès aux données ou le planificateur/l’appel d’outil ETL devra toutefois s’assurer que les lots sont traités dans l’ordre lorsque cela est possible.

## Report

Le report est un processus au cours duquel les données d’entrée ne sont pas encore suffisamment complètes pour être envoyées aux processus en aval, mais peuvent être utilisées ultérieurement. Les clients détermineront leur propre tolérance en ce qui concerne le fenêtrage des données pour la future mise en correspondance par rapport au coût du traitement. Cela permettra d’éclairer leur décision de mettre de côté les données et de les retraiter lors de la prochaine exécution de la transformation, dans l’espoir qu’elles pourront être enrichies et réconciliées/assemblées ultérieurement dans la fenêtre de rétention. Ce cycle se poursuit jusqu’à ce que la ligne soit suffisamment traitée ou qu’elle soit considérée comme obsolète et que tout investissement soit jugé inutile. Chaque itération générera des données différées qui constituent un sur-ensemble de toutes les données différées des itérations précédentes.

Actuellement, Adobe Experience Platform n’identifie pas les données différées. Les implémentations client doivent donc se fier aux configurations manuelles ETL et Dataset pour créer un autre jeu de données dans [!DNL Platform] reflétant le jeu de données source qui peut être utilisé pour conserver les données différées. Dans ce cas, les données différées sont similaires aux données instantanées. Dans chaque exécution de la transformation ETL, les données source sont combinées aux données différées et envoyées pour traitement.

## Journal des modifications

| Date | Action | Description |
| ---- | ------ | ----------- |
| 19/01/2019 | Suppression de la propriété « fields » des jeux de données | Les jeux de données comprenaient auparavant une propriété « fields » qui contenait une copie du schéma. Cette fonctionnalité ne doit plus être utilisée. Si la propriété « fields » est trouvée, elle doit être ignorée et la propriété « observedSchema » ou « schemaRef » utilisée à la place. |
| 15/03/2019 | Ajout de la propriété « schemaRef » aux jeux de données | La propriété « schemaRef » d’un jeu de données contient un URI référençant le XDM sur lequel le jeu de données est basé et représente tous les champs potentiels pouvant être utilisés par le jeu de données. |
| 15/03/2019 | Tous les identifiants d’utilisateur final mappent vers la propriété « identityMap ». | &quot;identityMap&quot; contient tous les identifiants uniques d’un sujet, tels que CRMID, ECID ou l’identifiant du programme de fidélité. Cette map est utilisée par le [[!DNL Identity Service]](../identity-service/home.md) pour résoudre toutes les identités connues et anonymes d’un sujet, formant un graphique d’identités unique pour chaque utilisateur final. |
| 30/05/2019 | Fin de vie et suppression de la propriété « schema » des jeux de données | La propriété « schema » du jeu de données fournissait un lien de référence vers le schéma à l’aide du point d’entrée `/xdms` obsolète dans l’API [!DNL Catalog] Cette valeur a été remplacée par un « schemaRef » qui fournit les valeurs « id », « version » et « contentType » du schéma, comme indiqué dans la nouvelle API [!DNL Schema Registry]. |
