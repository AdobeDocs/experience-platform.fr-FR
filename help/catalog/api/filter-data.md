---
keywords: Experience Platform;accueil;rubriques les plus consultées;filtre;Filtrer les données;Filtrer les données;période
solution: Experience Platform
title: Filtrage Des Données De Catalogue À L’Aide De Paramètres De Requête
description: Utilisez des paramètres de requête pour filtrer les données de réponse dans l’API Catalog Service et récupérer uniquement les informations dont vous avez besoin. Appliquez des filtres à vos appels API pour réduire la charge et améliorer les performances, assurant ainsi une récupération des données plus rapide et plus efficace.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 68%

---

# Filtrer [!DNL Catalog] données à l’aide de paramètres de requête

Pour améliorer les performances et récupérer des résultats pertinents, utilisez les paramètres de requête pour filtrer les données de réponse de l’API [!DNL Catalog Service].

Découvrez les méthodes de filtrage courantes pour les objets [!DNL Catalog] dans l’API. Utilisez ce document avec le [Guide du développeur du catalogue](getting-started.md) pour plus d’informations sur les interactions d’API. Pour obtenir des informations [!DNL Catalog Service] générales, consultez la [[!DNL Catalog] présentation](../home.md).

## Limiter les objets renvoyés {#limit-returned-objects}

Le paramètre de requête `limit` limite le nombre d’objets renvoyés dans une réponse. [!DNL Catalog] réponses suivent des limites prédéfinies :

* Si le paramètre `limit` n’est pas spécifié, le nombre maximal d’objets par réponse est de 20.
* Pour les requêtes des jeux de données, si `observableSchema` est demandé en utilisant le paramètre de requête `properties`, le nombre maximal de jeux de données renvoyés est de 20.
* Pour les jetons d’utilisateur, la limite maximale est de 1.
* Pour les jetons de service, la limite maximale est de 20.
* La limite globale pour les autres requêtes de catalogue est de 100 objets.
* Les valeurs de `limit` non valides (y compris `limit=0`) entraînent des réponses d’erreur de niveau 400 spécifiant des plages correctes.
* Les limites ou décalages transmis en tant que paramètres de requête sont prioritaires sur ceux des en-têtes.

**Format d’API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet [!DNL Catalog] à récupérer. Objets valides : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | Nombre entier spécifiant le nombre d’objets à renvoyer (plage : 1-100). |

**Requête**

La requête suivante récupère une liste de jeux de données en limitant la réponse à trois objets.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de jeux de données, limitée au nombre indiqué par le paramètre de requête `limit`.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limiter les propriétés affichées {#limit-displayed-properties}

Même lorsque le nombre d’objets renvoyés est filtré à l’aide du paramètre `limit`, les objets renvoyés eux-mêmes peuvent souvent contenir plus d’informations que nécessaire. Pour réduire davantage la charge sur le système, il est recommandé de filtrer les réponses afin d’inclure uniquement les propriétés dont vous avez besoin.

Le paramètre `properties` filtre les objets de réponse pour renvoyer uniquement un ensemble de propriétés spécifiées. Ce paramètre peut être défini pour renvoyer une ou plusieurs propriétés.

Le paramètre `properties` peut accepter n&#39;importe quelle propriété d&#39;objet de niveau. Les `sampleKey` peuvent être extraites à l’aide de `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | Le nom d’un attribut à inclure dans le corps de la réponse. |
| `{OBJECT_ID}` | Identifiant unique d’un objet [!DNL Catalog] spécifique récupéré. |

**Requête**

La requête suivante récupère une liste de jeux de données. La liste de noms de propriétés séparés par des virgules fournie sous le paramètre `properties` indique les propriétés à renvoyer dans la réponse. Un paramètre `limit` est également inclus pour limiter le nombre de jeux de données renvoyés. Si la requête n’incluait pas de paramètre `limit`, la réponse contiendrait 20 objets maximum.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets [!DNL Catalog] avec seulement les propriétés demandées affichées.

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

En fonction de la réponse ci-dessus, vous pouvez en déduire ce qui suit :

* Si une ou plusieurs propriétés demandées sont absentes d’un objet, seules les propriétés demandées qu’il inclut seront affichées. (`Dataset1`)
* Si un objet n’inclut aucune des propriétés demandées, il apparaîtra comme un objet vide. (`Dataset2`)
* Un jeu de données peut renvoyer une propriété demandée en tant qu’objet vide s’il contient la propriété, mais sans aucune valeur. (`Dataset3`)
* Sinon, le jeu de données affichera la valeur complète de toutes les propriétés demandées. (`Dataset4`)

>[!NOTE]
>
>Dans la propriété `schemaRef` de chaque jeu de données, le numéro de version indique la dernière version mineure du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../xdm/api/getting-started.md#versioning) du guide de l’API XDM.

## Décalage de l’index de départ de la liste de réponses {#offset-starting-index}

Le paramètre de requête `start` décale la liste de réponses vers l’avant d’un nombre spécifié, en utilisant une numérotation à partir de zéro. Par exemple, `start=2` décalerait la réponse pour qu’elle commence à partir du troisième objet répertorié.

Si le paramètre `start` n’est associé à aucun paramètre `limit`, le nombre maximal d’objets renvoyés est de 20.

**Format d’API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type d’objets Catalog à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | Un entier indiquant le nombre d’objets de décalage de la réponse. |

**Requête**

La requête suivante récupère une liste de jeux de données, décalée au cinquième objet (`start=4`) et qui limite la réponse à deux jeux de données renvoyés (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un objet JSON contenant deux éléments de niveau supérieur (`limit=2`), un pour chaque jeu de données ainsi que leurs détails (les détails ont été condensés dans l’exemple). La réponse est décalée de quatre (`start=4`), ce qui signifie que les jeux de données affichés sont chronologiquement les cinquième et sixième.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrage par balise

Certains objets Catalog prennent en charge l’utilisation d’un attribut `tags`. Les balises peuvent joindre des informations à un objet, puis être utilisées ultérieurement pour récupérer cet objet. Le choix des balises à utiliser et la manière de les appliquer dépendent de vos processus organisationnels.

Quelques limites doivent être prises en compte lors de l’utilisation de balises :

* Les seuls objets Catalog qui prennent actuellement en charge les balises sont les jeux de données, les lots et les connexions.
* Les noms de balises sont propres à votre organisation.
* Les processus Adobe peuvent se servir de balises pour certains comportements. Le préfixe standard « adobe » est ajouté au nom de ces balises. Par conséquent, vous devriez éviter cette pratique lors de la déclaration des noms de balise.
* Les noms de balise suivants sont réservés à l’utilisation dans [!DNL Experience Platform] et ne peuvent donc pas être déclarés comme nom de balise pour votre organisation :
   * `unifiedProfile` : ce nom de balise est réservé aux jeux de données à ingérer par [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity` : ce nom de balise est réservé aux jeux de données à ingérer par [[!DNL Identity Service]](../../identity-service/home.md).

Vous trouverez ci-dessous un exemple de jeu de données contenant une propriété `tags`. Les balises de cette propriété prennent la forme de paires clé-valeur, où chaque valeur de balise apparaît sous la forme d’une matrice contenant une seule chaîne :

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
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

Les valeurs du paramètre `tags` prennent la forme de paires clé-valeur sous le format `{TAG_NAME}:{TAG_VALUE}`. Plusieurs paires clé-valeur peuvent être fournies sous la forme d’une liste dont les valeurs sont séparées par des virgules. Lorsque plusieurs balises sont fournies, l’existence d’une relation ET est supposée.

Le paramètre prend en charge les caractères génériques (`*`) pour les valeurs de balise. Par exemple, une chaîne de recherche de `test*` renvoie tout objet dont la valeur de balise commence par « test ». Une chaîne de recherche composée uniquement d’un caractère générique peut être utilisée pour filtrer les objets selon qu’ils contiennent ou non une balise spécifique, quelle que soit sa valeur.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Le nom de la balise à utiliser pour filtrer. |
| `{TAG_VALUE}` | La valeur de la balise à utiliser pour filtrer. Prend en charge les caractères génériques (`*`). |

**Requête**

La requête suivante récupère une liste de jeux de données, filtrée à l’aide d’une balise ayant une valeur spécifique ET d’une deuxième balise présente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de jeux de données qui contiennent `sampleTag` d’une valeur de « 123456 », ET `secondTag` de n’importe quelle valeur. À moins qu’une limite ne soit également spécifiée, la réponse contient 20 objets maximum.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
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
    }
}
```

## Filtrage par période

Certains points d’entrée de l’API [!DNL Catalog] disposent de paramètres de requête qui permettent les requêtes à intervalles de temps, le plus souvent dans le cas de dates.

**Format d’API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Paramètre | Description |
| --- | --- |
| `{TIMESTAMP }` | Un entier d’horodatage en heure Unix. |

**Requête**

La requête suivante récupère une liste de lots créés au cours du mois d’avril 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste d’objets [!DNL Catalog] qui se trouvent dans la période spécifiée. À moins qu’une limite ne soit également spécifiée, la réponse contient 20 objets maximum.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Tri par propriété

Le paramètre de requête `orderBy` vous permet de trier (organiser) les données de réponse en fonction d’une valeur de propriété spécifiée. Ce paramètre requiert une « direction » (`asc` pour un ordre croissant ou `desc` pour un ordre décroissant), suivie par deux points (`:`) puis une propriété selon laquelle trier les résultats. Si aucune direction n’est spécifiée, l’ordre par défaut est croissant.

Plusieurs propriétés de tri peuvent être fournies dans une liste aux valeurs séparées par des virgules. Si la première propriété de tri génère plusieurs objets qui contiennent la même valeur pour cette propriété, la deuxième propriété de tri est ensuite utilisée pour trier les objets correspondants.

Prenons pour exemple la requête suivante : `orderBy=name,desc:created`. Les résultats sont triés par ordre croissant en fonction de la première propriété de tri `name`. Dans les cas où plusieurs enregistrements partagent la même propriété `name`, ces enregistrements correspondants sont ensuite triés par la deuxième propriété de tri `created`. Si aucun enregistrement renvoyé ne partage le même `name`, la propriété `created` n’a aucune influence sur le tri.


**Format d’API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type d’objets Catalog à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Le nom d’une propriété selon laquelle trier les résultats. |

**Requête**

La requête suivante récupère une liste de jeux de données triés par leur propriété `name`. Si des jeux de données partageaient le même `name`, ces jeux de données seraient à leur tour classés selon leur propriété `updated` dans l’ordre décroissant.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste d’objets [!DNL Catalog] qui sont triés en fonction du paramètre `orderBy` . À moins qu’une limite ne soit également spécifiée, la réponse contient 20 objets maximum.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Filtrage par propriété

[!DNL Catalog] propose deux méthodes de filtrage par propriété, qui sont décrites plus en détail dans les sections suivantes :

* [Utilisation de filtres simples](#using-simple-filters) : filtrez pour qu’une propriété spécifique corresponde à une valeur spécifique.
* [Utilisation du paramètre de propriété](#using-the-property-parameter) : utilisez des expressions conditionnelles pour un filtre se basant sur l’existence ou non d’une propriété ou sur la correspondance, la ressemblance ou la possibilité de comparer ou non la valeur d’une propriété à une autre valeur spécifiée ou à une expression régulière.

>[!NOTE]
>
>Tout attribut d’un objet Catalog peut être utilisé pour filtrer les résultats dans l’API Catalog Service.

### Utilisation de filtres simples {#using-simple-filters}

Les filtres simples vous permettent de filtrer les réponses en fonction de valeurs de propriété spécifiques. Un filtre simple prend la forme `{PROPERTY_NAME}={VALUE}`.

Par exemple, la requête `name=exampleName` renvoie uniquement les objets dont la propriété `name` contient une valeur « exampleName ». En revanche, la requête `name=!exampleName` renvoie uniquement les objets dont la propriété `name` **n’est pas** « exampleName ».

En outre, les filtres simples prennent en charge la capacité de formuler des requêtes pour récupérer plusieurs valeurs pour une seule propriété. Lorsque plusieurs valeurs sont fournies, la réponse renvoie des objets dont la propriété correspond à **n’importe quelle** valeur de la liste fournie. Vous pouvez inverser une requête à plusieurs valeurs en ajoutant un caractère `!` en préfixe à la liste, ce qui renverra uniquement les objets dont la valeur de propriété **n’est pas** dans la liste fournie (par exemple `name=!exampleName,anotherName`).

**Format d’API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Le nom de la propriété dont la valeur est celle que vous souhaitez utiliser pour filtrer. |
| `{VALUE}` | Une valeur de propriété qui détermine les résultats à inclure (ou à exclure, selon la requête). |

**Requête**

La requête suivante récupère une liste de jeux de données filtrée pour inclure uniquement les jeux de données dont la propriété `name` possède une valeur « exampleName » ou « anotherName ».

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste de jeux de données excluant ceux dont le `name` est « exampleName » ou « anotherName ». À moins qu’une limite ne soit également spécifiée, la réponse contient 20 objets maximum.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

### Utilisation du paramètre `property` {#using-the-property-parameter}

Le paramètre de requête `property` offre plus de flexibilité pour le filtrage basé sur les propriétés que les filtres simples. En complément du filtrage selon qu’une propriété possède ou non une valeur spécifique, le paramètre `property`peut utiliser d’autres opérateurs de comparaison (tels que « more-than »,`>`, et « less-than », `<`), ainsi que des expressions régulières pour filtrer selon les valeurs de propriété. Il peut également filtrer selon l’existence ou l’absence d’une propriété, quelle que soit sa valeur.

Utilisez une esperluette (`&`) pour combiner plusieurs filtres et affiner votre requête dans une seule requête. Lorsque vous filtrez par plusieurs champs, une relation de `AND` est appliquée par défaut.

>[!NOTE]
>
>Si vous combinez plusieurs paramètres de `property` dans une seule requête, au moins l’un d’eux doit s’appliquer au champ `id` ou `created`. La requête suivante renvoie des objets où `id` est `abc123` **AND** `name` n’est pas `test` :
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

Si vous utilisez plusieurs paramètres de `property` sur le même champ, seul le dernier paramètre spécifié prend effet.

>[!IMPORTANT]
>
>Vous **ne pouvez pas** utiliser un seul paramètre de `property` pour filtrer plusieurs champs à la fois. Chaque champ doit avoir son propre paramètre `property`. L’exemple suivant (`property=id>abc,name==myDataset`) n’est **pas** autorisé, car il tente d’appliquer des conditions aux `id` et aux `name` dans un **paramètre de `property` unique**.

Le paramètre `property` peut accepter n&#39;importe quelle propriété d&#39;objet de niveau. `sampleKey` pouvez être utilisé pour le filtrage à l’aide de `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à récupérer. Les objets valides sont : <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Une instruction conditionnelle qui indique la propriété pour laquelle formuler une requête et la manière dont sa valeur doit être évaluée. Vous en trouverez des exemples ci-dessous. |

La valeur du paramètre `property` prend en charge plusieurs types différents d’instructions conditionnelles. Le tableau suivant décrit la syntaxe de base pour les instructions prises en charge :

| Symbole(s) | Description | Exemple |
| --- | --- | --- |
| (Aucun) | Indiquer le nom de la propriété sans opérateur renvoie uniquement les objets dans lesquels la propriété existe, et ce quelle que soit sa valeur. | `property=name` |
| ! | Ajouter le préfixe « `!` » à la valeur d’un paramètre `property` renvoie uniquement les objets dans lesquels la propriété **n’existe pas**. | `property=!name` |
| ~ | Renvoie uniquement les objets dont les valeurs de propriété (chaîne) correspondent à une expression régulière fournie après le signe tilde (`~`). | `property=name~^example` |
| == | Renvoie uniquement les objets dont les valeurs de propriété correspond exactement à la chaîne fournie après le signe double égal (`==`). | `property=name==exampleName` |
| != | Renvoie uniquement les objets dont les valeurs de propriété **ne correspondent pas** à la chaîne fournie après le signe différent (`!=`). | `property=name!=exampleName` |
| &lt; | Renvoie uniquement les objets dont les valeurs de propriété sont inférieures (mais pas égales) à un montant donné. | `property=version<1.0.0` |
| &lt;= | Renvoie uniquement les objets dont les valeurs de propriété sont inférieures (ou égales) à un montant donné. | `property=version<=1.0.0` |
| > | Renvoie uniquement les objets dont les valeurs de propriété sont supérieures (mais pas égales) à un montant donné. | `property=version>1.0.0` |
| >= | Renvoie uniquement les objets dont les valeurs de propriété sont supérieures (ou égales) à un montant donné. | `property=version>=1.0.0` |
| * | Un caractère générique s’applique à n’importe quelle propriété de chaîne et correspond à n’importe quelle séquence de caractères. Utilisez `**` pour échapper un astérisque littéral. | `property=name==te*st` |
| &amp; | Combine plusieurs paramètres de `property` avec une relation `AND` entre eux. | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>La propriété `name` prend en charge l’utilisation d’un `*` de caractères génériques, soit comme chaîne de recherche complète, soit comme partie de celle-ci. Les caractères génériques correspondent à des caractères vides, de sorte que la chaîne de recherche `te*st` correspond à la valeur « test ». Les astérisques sont évités en les doublant (`**`). Un double astérisque dans une chaîne de recherche représente un astérisque unique sous forme de chaîne littérale.

**Requête**

La requête suivante renvoie tous les jeux de données dont le numéro de version est supérieur à 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie contient une liste de jeux de données dont les numéros de version sont supérieurs à 1.0.3. Si aucune limite n’est spécifiée, la réponse contient 20 objets maximum.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Filtrer des tableaux avec le paramètre de propriété {#filter-arrays}

Utilisez des opérateurs d’égalité et d’inégalité pour inclure ou exclure des valeurs spécifiques lors du filtrage des résultats en fonction des propriétés du tableau.

### Filtres d’égalité {#equality-filters}

Pour filtrer un champ de tableau selon plusieurs valeurs, utilisez des paramètres de propriété distincts pour chaque valeur. Utilisez des filtres d’égalité pour renvoyer uniquement les entrées des données du tableau qui correspondent aux valeurs spécifiées.

>[!NOTE]
>
>L’obligation d’inclure des `id` ou des `created` lors du filtrage de plusieurs champs ne s’applique **pas** lors du filtrage de plusieurs valeurs dans un champ de tableau.

L’exemple de requête ci-dessous renvoie uniquement les résultats du tableau qui comprend à la fois `val1` et `val2`.

**Format d’API**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### Filtres d’inégalité {#inequality-filters}

Utilisez des opérateurs d’inégalité (`!=`) sur un champ de tableau pour exclure toute entrée dans les données où le tableau contient les valeurs spécifiées.

**Format d’API**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

Cette requête renvoie des documents où arrayField ne contient ni `val1` ni `val2`.

### Égalité et limites des filtres d’inégalité {#equality-inequality-limitations}

Vous ne pouvez pas appliquer à la fois l’égalité (`=`) et l’inégalité (`!=`) au même champ dans une seule requête.
