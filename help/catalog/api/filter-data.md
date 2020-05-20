---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filtrage des données du catalogue à l’aide des paramètres de requête
topic: developer guide
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 1%

---


# Filtrage des données du catalogue à l’aide des paramètres de requête

L’API du service de catalogue permet de filtrer les données de réponse à l’aide des paramètres de requête de demande. Une des meilleures pratiques pour le catalogue consiste à utiliser des filtres dans tous les appels d’API, car ils réduisent la charge sur l’API et contribuent à améliorer les performances globales.

Ce document décrit les méthodes les plus courantes de filtrage des objets de catalogue dans l’API. Il est recommandé de faire référence à ce document lors de la lecture du guide [du développeur du](getting-started.md) catalogue pour en savoir plus sur la façon d’interagir avec l’API du catalogue. Pour plus d’informations générales sur le service de catalogue, voir la présentation [du](../home.md)catalogue.

## Limiter les objets renvoyés

Le paramètre `limit` requête limite le nombre d’objets renvoyés dans une réponse. Les réponses au catalogue sont automatiquement mesurées en fonction des limites configurées :

* Si aucun `limit` paramètre n’est spécifié, le nombre maximal d’objets par charge utile de réponse est de 20.
* Pour les requêtes de jeux de données, si `observableSchema` vous en faites la demande à l’aide du paramètre `properties` requête, le nombre maximal de jeux de données renvoyé est 20.
* La limite globale pour toutes les autres requêtes de catalogue est de 100 objets.
* Des `limit` paramètres non valides (y compris `limit=0`) génèrent des réponses d’erreur de 400 niveaux qui indiquent les plages appropriées.
* Les limites ou décalages transmis en tant que paramètres de requête sont prioritaires sur ceux transmis en tant qu’en-têtes.

**Format d’API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Entier indiquant le nombre d’objets à renvoyer, compris entre 1 et 100. |

**Requête**

La requête suivante récupère une liste de jeux de données tout en limitant la réponse à trois objets.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de jeux de données, limitée au nombre indiqué par le paramètre de `limit` requête.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limiter les propriétés affichées

Même lors du filtrage du nombre d’objets renvoyés à l’aide du `limit` paramètre, les objets renvoyés eux-mêmes peuvent souvent contenir plus d’informations que nécessaire. Pour réduire davantage la charge sur le système, il est recommandé de filtrer les réponses afin d’inclure uniquement les propriétés dont vous avez besoin.

Le `properties` paramètre filtres les objets de réponse à renvoyer uniquement un jeu de propriétés spécifiées. Le paramètre peut être défini pour renvoyer une ou plusieurs propriétés.

Le `properties` paramètre accepte uniquement les propriétés d’objet de niveau supérieur, ce qui signifie que pour l’objet exemple suivant, vous pouvez appliquer des filtres pour `name`, `description`et `subItem`mais PAS pour `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Format d’API**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Nom d’un attribut à inclure dans le corps de la réponse. |
| `{OBJECT_ID}` | Identificateur unique d’un objet Catalog spécifique récupéré. |

**Requête**

La requête suivante récupère une liste de jeux de données. La liste séparée par des virgules des noms de propriétés fournie sous le `properties` paramètre indique les propriétés à renvoyer dans la réponse. Un `limit` paramètre est également inclus, ce qui limite le nombre de jeux de données renvoyés. Si la requête n’incluait pas de `limit` paramètre, la réponse contiendrait un maximum de 20 objets.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d&#39;objets Catalog avec uniquement les propriétés demandées affichées.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

En fonction de la réponse ci-dessus, les éléments suivants peuvent être déduits :

* Si des propriétés demandées sont manquantes pour un objet, seules les propriétés demandées qu’il contient sont affichées. (`Dataset1`)
* Si un objet n’inclut aucune des propriétés demandées, il apparaît comme un objet vide. (`Dataset2`)
* Un jeu de données peut renvoyer une propriété demandée en tant qu’objet vide s’il contient la propriété mais qu’il n’y a aucune valeur. (`Dataset3`)
* Sinon, le jeu de données affichera la valeur complète de toutes les propriétés demandées. (`Dataset4`)

## Décaler l&#39;index de début de la liste de réponse

Le paramètre `start` requête compense la liste de réponse vers l’avant par un nombre spécifié, en utilisant une numérotation à base zéro. Par exemple, `start=2` décalerait la réponse au début sur le troisième objet répertorié.

Si le `start` paramètre n’est pas associé à un `limit` paramètre, le nombre maximal d’objets renvoyés est de 20.

**Format d’API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Entier indiquant le nombre d’objets de décalage de la réponse. |

**Requête**

La requête suivante récupère une liste de jeux de données, en la décalant sur le cinquième objet (`start=4`) et en limitant la réponse à deux jeux de données renvoyés (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un objet JSON contenant deux éléments de niveau supérieur (`limit=2`), un pour chaque jeu de données et leurs détails (les détails ont été condensés dans l’exemple). La réponse est décalée de quatre (`start=4`), ce qui signifie que les jeux de données indiqués sont les numéros cinq et six chronologiquement.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrage par balise

Certains objets Catalog prennent en charge l’utilisation d’un `tags` attribut. Les balises peuvent joindre des informations à un objet, puis être utilisées ultérieurement pour récupérer cet objet. Le choix des balises à utiliser et de la manière de les appliquer dépend de vos processus d’entreprise.

Il existe quelques limites à prendre en compte lors de l’utilisation de balises :

* Les seuls objets de catalogue qui prennent actuellement en charge les balises sont les jeux de données, les lots et les connexions.
* Les noms de balise sont propres à votre organisation IMS.
* Les processus Adobe peuvent utiliser des balises pour certains comportements. Les noms de ces balises sont précédés du préfixe &quot;adobe&quot; comme standard. Par conséquent, vous devez éviter cette convention lors de la déclaration des noms de balises.
* Les noms de balise suivants sont réservés à l’utilisation sur la plate-forme d’expérience et ne peuvent donc pas être déclarés en tant que nom de balise pour votre organisation :
   * `unifiedProfile`: Ce nom de balise est réservé pour que les jeux de données soient assimilés par le Profil [client](../../profile/home.md)en temps réel.
   * `unifiedIdentity`: Ce nom de balise est réservé pour que les jeux de données soient assimilés par [Identity Service](../../identity-service/home.md).

Vous trouverez ci-dessous un exemple de jeu de données contenant une `tags` propriété. Les balises de cette propriété prennent la forme de paires clé-valeur, chaque valeur de balise apparaissant sous la forme d’un tableau contenant une seule chaîne :

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**Format d’API**

Les valeurs du `tags` paramètre prennent la forme de paires clé-valeur, en utilisant le format `{TAG_NAME}:{TAG_VALUE}`. Plusieurs paires clé-valeur peuvent être fournies sous la forme d’une liste séparée par des virgules. Lorsque plusieurs balises sont fournies, une relation ET est supposée.

Le paramètre prend en charge les caractères génériques (`*`) pour les valeurs de balise. Par exemple, une chaîne de recherche de `test*` renvoie tout objet dont la valeur de balise commence par &quot;test&quot;. Une chaîne de recherche composée uniquement d’un caractère générique peut être utilisée pour filtrer les objets selon qu’ils contiennent ou non une balise spécifique, quelle que soit sa valeur.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nom de la balise à filtrer. |
| `{TAG_VALUE}` | Valeur de la balise par laquelle filtrer. Prend en charge les caractères génériques (`*`). |

**Requête**

La requête suivante récupère une liste de jeux de données, en filtrant par une balise ayant une valeur spécifique ET la deuxième balise étant présente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de jeux de données qui contiennent `sampleTag` la valeur &quot;123456&quot;, ET `secondTag` toute valeur. A moins qu’une limite ne soit également spécifiée, la réponse contient un maximum de 20 objets.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrage par période

Certains points de terminaison de l’API Catalogue comportent des paramètres de requête qui autorisent les requêtes de plage, le plus souvent dans le cas de dates.

**Format d’API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Paramètre | Description |
| --- | --- |
| `{TIMESTAMP }` | Entier datetime dans Unix Epoch time. |

**Requête**

La requête suivante récupère une liste de lots créés au cours du mois d’avril 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste d’objets Catalog compris dans la plage de dates spécifiée. A moins qu’une limite ne soit également spécifiée, la réponse contient un maximum de 20 objets.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Trier par propriété

Le paramètre `orderBy` requête vous permet de trier (trier) les données de réponse en fonction d’une valeur de propriété spécifiée. Ce paramètre requiert une &quot;direction&quot; (`asc` pour l’ordre croissant ou `desc` pour l’ordre décroissant), suivie d’un deux-points (`:`), puis une propriété pour trier les résultats. Si aucune direction n&#39;est spécifiée, la direction par défaut est ascendante.

Plusieurs propriétés de tri peuvent être fournies dans une liste séparée par des virgules. Si la première propriété de tri génère plusieurs objets qui contiennent la même valeur pour cette propriété, la seconde propriété de tri est ensuite utilisée pour trier les objets correspondants.

Par exemple, tenez compte de la requête suivante : `orderBy=name,desc:created`. Les résultats sont triés par ordre croissant en fonction de la première propriété de tri `name`. Dans les cas où plusieurs enregistrements partagent la même `name` propriété, ces enregistrements correspondants sont ensuite triés par la seconde propriété de tri, `created`. Si aucun enregistrement renvoyé ne partage le même `name`, la `created` propriété n’est pas prise en compte dans le tri.


**Format d’API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nom d’une propriété pour trier les résultats. |

**Requête**

La requête suivante récupère une liste de jeux de données triée par leur `name` propriété. Si des jeux de données partagent le même `name`jeu, ces jeux de données sont à leur tour classés par leur `updated` propriété dans l’ordre décroissant.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive contient une liste d’objets Catalog triés en fonction du `orderBy` paramètre. A moins qu’une limite ne soit également spécifiée, la réponse contient un maximum de 20 objets.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrage par propriété

Le catalogue propose deux méthodes de filtrage par propriété, décrites plus en détail dans les sections suivantes :

* [Utilisation de filtres](#using-simple-filters)simples : Vous pouvez filtrer selon si une propriété spécifique correspond à une valeur spécifique.
* [Utilisation du paramètre](#using-the-property-parameter)de propriété : Utilisez des expressions conditionnelles pour filtrer selon si une propriété existe ou si la valeur d’une propriété correspond, se rapproche ou se compare à une autre valeur spécifiée ou à une expression régulière.

### Utilisation de filtres simples {#using-simple-filters}

Les filtres simples vous permettent de filtrer les réponses en fonction de valeurs de propriété spécifiques. Un filtre simple prend la forme de `{PROPERTY_NAME}={VALUE}`.

Par exemple, la requête `name=exampleName` renvoie uniquement les objets dont `name` la propriété contient la valeur &quot;exampleName&quot;. En revanche, la requête `name=!exampleName` renvoie uniquement les objets dont la `name` propriété **** n’est pas &quot;exampleName&quot;.

En outre, les filtres simples prennent en charge la requête de plusieurs valeurs pour une seule propriété. Lorsque plusieurs valeurs sont fournies, la réponse renvoie des objets dont la propriété correspond à **l’une** des valeurs de la liste fournie. Vous pouvez inverser une requête à plusieurs valeurs en préfixant un `!` caractère à la liste, en renvoyant uniquement les objets dont la valeur de propriété **ne figure pas** dans la liste fournie (par exemple `name=!exampleName,anotherName`).

**Format d’API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nom de la propriété dont vous souhaitez filtrer la valeur. |
| `{VALUE}` | Valeur de propriété qui détermine quels résultats inclure (ou exclure, selon la requête). |

**Requête**

La requête suivante récupère une liste de jeux de données, filtrée pour inclure uniquement les jeux de données dont la `name` propriété a la valeur &quot;exampleName&quot; ou &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste de jeux de données, à l&#39;exclusion de tous les jeux de données dont `name` le nom est &quot;exampleName&quot; ou &quot;anotherName&quot;. A moins qu’une limite ne soit également spécifiée, la réponse contient un maximum de 20 objets.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### Utilisation du `property` paramètre {#using-the-property-parameter}

Le paramètre de `property` requête offre davantage de flexibilité pour le filtrage basé sur les propriétés que les filtres simples. Outre le filtrage selon si une propriété possède une valeur spécifique, le `property` paramètre peut utiliser d’autres opérateurs de comparaison (tels que &quot;plus que&quot; (`>`) et &quot;moins que&quot; (`<`)), ainsi que des expressions régulières pour filtrer par valeurs de propriété. Il peut également filtrer selon qu’une propriété existe ou non, quelle que soit sa valeur.

Le `property` paramètre accepte uniquement les propriétés d’objet de niveau supérieur, ce qui signifie que pour l’objet exemple suivant, vous pouvez filtrer par propriété pour `name`, `description`et `subItem`, mais PAS pour `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Format d’API**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à récupérer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | expression conditionnelle qui indique la propriété à requête et comment sa valeur doit être évaluée. Vous trouverez des exemples ci-dessous. |

La valeur du `property` paramètre prend en charge différents types d’expressions conditionnelles. Le tableau suivant décrit la syntaxe de base des expressions prises en charge :

| Symbole(s) | Description | Exemple |
| --- | --- | --- |
| (Aucun) | La mention du nom de la propriété sans opérateur renvoie uniquement les objets où la propriété existe, quelle que soit sa valeur. | `property=name` |
| ! | La préfixation d’un &quot;`!`&quot; à la valeur d’un `property` paramètre renvoie uniquement les objets dans lesquels la propriété **n’existe pas** . | `property=!name` |
| ~ | Renvoie uniquement les objets dont les valeurs de propriété (chaîne) correspondent à une expression régulière fournie après le symbole tilde (`~`). | `property=name~^example` |
| == | Renvoie uniquement les objets dont les valeurs de propriété correspondent exactement à la chaîne fournie après le symbole doublon-equals (`==`). | `property=name==exampleName` |
| != | Renvoie uniquement les objets dont les valeurs de propriété **ne correspondent pas** à la chaîne fournie après le symbole not-equals (`!=`). | `property=name!=exampleName` |
| &lt; | Renvoie uniquement les objets dont les valeurs de propriété sont inférieures (mais non égales) à un montant indiqué. | `property=version<1.0.0` |
| &lt;= | Renvoie uniquement les objets dont les valeurs de propriété sont inférieures (ou égales à) à un montant indiqué. | `property=version<=1.0.0` |
| > | Renvoie uniquement les objets dont les valeurs de propriété sont supérieures (mais non égales) à un montant indiqué. | `property=version>1.0.0` |
| >= | Renvoie uniquement les objets dont les valeurs de propriété sont supérieures (ou égales à) à un montant indiqué. | `property=version>=1.0.0` |

>[!NOTE] La `name` propriété prend en charge l’utilisation d’un caractère générique `*`, sous la forme d’une chaîne de recherche complète ou d’une partie de celle-ci. Les caractères génériques correspondent à des caractères vides, de sorte que la chaîne de recherche `te*st` corresponde à la valeur &quot;test&quot;. Les astérisques sont évités en les doublant (`**`). Un doublon-astérisque dans une chaîne de recherche représente un astérisque unique comme chaîne littérale.

**Requête**

La requête suivante renvoie tous les jeux de données dont le numéro de version est supérieur à 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste de jeux de données dont les numéros de version sont supérieurs à 1.0.3. A moins qu&#39;une limite ne soit également spécifiée, la réponse contient un maximum de 20 objets.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Combiner plusieurs filtres

A l’aide d’une esperluette (`&`), vous pouvez combiner plusieurs filtres dans une même requête. Lorsque d’autres conditions sont ajoutées à une requête, une relation ET est supposée.

**Format d’API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
