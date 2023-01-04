---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Points de terminaison de l’API de projection Edge
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform vous permet de proposer des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs canaux en temps réel, en rendant les données appropriées facilement disponibles et mises à jour en continu au fur et à mesure des changements. Pour ce faire, il utilise des périphéries, un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 86%

---

# Configurations de projection Edge et points d’entrée de destinations

Afin d’offrir à vos clients des expériences coordonnées, cohérentes et personnalisées sur plusieurs canaux en temps réel, les bonnes données doivent être facilement disponibles et mises à jour en continu, au fur et à mesure des changements. Adobe Experience Platform permet cet accès aux données en temps réel grâce à l’utilisation de ce que l’on appelle les périphéries. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles qu’Adobe Target et Adobe Campaign utilisent des périphéries afin d’offrir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie. Ce guide fournit des instructions détaillées sur l’utilisation de la variable [!DNL Real-Time Customer Profile] API pour travailler avec des projections de périphérie, y compris des destinations et des configurations.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

>[!NOTE]
>
>Les requêtes contenant un payload (POST, PUT, PATCH) nécessitent un `Content-Type` en-tête . Plus d’un `Content-Type` est utilisé dans ce document. Veuillez prêter une attention particulière aux en-têtes des exemples d’appels pour vous assurer que vous utilisez les `Content-Type` pour chaque requête.

## Destinations de projection

Vous pouvez acheminer une projection vers une ou plusieurs périphéries en précisant les emplacements vers lesquels les données doivent être envoyées. Chaque destination de projection créée possède un ID unique qui est ensuite utilisé pour créer la configuration de projection.

### Liste de toutes les destinations

Vous pouvez lister les destinations de périphérie déjà créées pour votre organisation en effectuant une requête GET sur le point de terminaison `/config/destinations`.

**Format d’API**

```http
GET /config/destinations
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse inclut un tableau `projectionDestinations` qui contient les détails de chaque destination affichés sous la forme d’un objet individuel du tableau. Si aucune projection n’a été définie, le tableau `projectionDestinations` est vide.

>[!NOTE]
>
>Cette réponse a été raccourcie pour des raisons de place et n’affiche que deux destinations.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Propriété | Description |
|---|---|
| `_links.self.href` | Au niveau supérieur, correspond au chemin d’accès utilisé pour effectuer la requête GET. Au sein de chaque objet de destination, ce chemin d’accès peut être utilisé dans une requête GET pour rechercher directement les détails d’une destination spécifique. |
| `id` | Au sein de chaque objet de destination, l’`"id"` affiche l’ID unique généré par le système et en lecture seule de la destination. Cet identifiant est utilisé lorsque vous faites référence à une destination spécifique et que vous créez des configurations de projection. |

Pour plus d’informations concernant les attributs d’une destination individuelle, veuillez consulter la section de [création d’une destination](#create-a-destination) qui suit.

### Création d’une destination {#create-a-destination}

Si la destination dont vous avez besoin n’existe pas déjà, vous pouvez créer une nouvelle destination de projection en effectuant une requête POST sur le point de terminaison `/config/destinations`.

**Format d’API**

```http
POST /config/destinations
```

**Requête**

La requête suivante crée une nouvelle destination de périphérie.

>[!NOTE]
>
>La requête POST pour créer une destination nécessite un en-tête `Content-Type` spécifique, comme indiqué ci-dessous. L’utilisation d’un en-tête `Content-Type` incorrect entraîne un état HTTP 415 (Unsupported Media Type).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| Propriété | Description |
|---|---|
| `type` **(Obligatoire)** | Type de destination à créer. La seule valeur acceptée, « EDGE », crée une destination de périphérie. |
| `dataCenters` **(Obligatoire)** | Tableau de chaînes qui répertorie les périphéries vers lesquelles les projections doivent être acheminées. Peut contenir une ou plusieurs des valeurs suivantes : « OR1 » - États-Unis de l’Ouest, « VA5 » - États-Unis de l’Est, « NLD1 » - EMEA. |
| `ttl` **(Obligatoire)** | Indique l’expiration de projection. Plage de valeurs acceptée : 600 à 604800. Valeur par défaut : 3600. |
| `replicationPolicy` **(Obligatoire)** | Définit le comportement de la réplication des données du hub aux périphéries.  Valeurs prises en charge : PROCATIVE, RÉACTIVE. Valeur par défaut : RÉACTIVE. |

**Réponse**

Une réponse réussie renvoie les détails de la destination de périphérie que vous venez de créer, y compris l’ID unique généré par le système et en lecture seule (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Propriété | Description |
|---|---|
| `self.href` | Ce chemin d’accès est utilisé pour rechercher (GET) la destination directement et peut également être utilisé pour mettre à jour (PUT) ou supprimer (DELETE) la destination. |
| `id` | L’identifiant unique généré par le système et en lecture seule de la destination. Cet identifiant est utilisé pour faire référence directement à la destination et lors de la création de configurations de projection. |
| `version` | Cette valeur en lecture seule de la version actuelle de la destination. Lorsqu’une destination est mise à jour, le numéro de version s’incrémente automatiquement. |

### Affichage d’une destination

Si vous connaissez l’ID unique d’une destination de projection, vous pouvez réaliser une requête de recherche pour en afficher les détails. Vous pouvez effectuer ceci à l’aide d’une requête GET sur le point de terminaison `/config/destinations` et inclure l’identifiant de la destination dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | L’ID unique de la destination de projection que vous souhaitez afficher. |

**Requête**

La requête suivante effectue une recherche (GET) pour afficher la destination de l’identifiant fourni dans le chemin d’accès de la requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet de réponse affiche les détails de la destination de projection. L’attribut `id` doit correspondre à l’identifiant de la destination de projection fourni dans la requête.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Mise à jour d’une destination

Vous pouvez mettre à jour une destination existante en effectuant une requête PUT sur le point de terminaison `/config/destinations` et en incluant l’identifiant de la destination à mettre à jour dans le chemin d’accès de la requête. Cette opération consiste essentiellement à réécrire la destination. Par conséquent, les mêmes attributs doivent être fournis dans le corps de la requête que ceux fournis lors de la création d’une nouvelle destination.

>[!CAUTION]
>
>La réponse de l’API à la demande de mise à jour est immédiate, c’est pourquoi les modifications sont appliquées de manière asynchrone aux projections. En d’autres termes, il y a une différence de temps entre le moment où la mise à jour de la définition de la destination est effectuée et le moment où elle est appliquée.

**Format d’API**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | L’ID unique de la destination de projection que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour la destination existante pour y inclure un second emplacement (`dataCenters`).

>[!IMPORTANT]
>
>La requête PUT nécessite un en-tête `Content-Type` spécifique, comme illustré ci-dessous. L’utilisation d’un en-tête `Content-Type` incorrect entraîne un état HTTP 415 (Unsupported Media Type).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Propriété | Description |
|---|---|
| `currentVersion` | La version actuelle de la destination existante. La valeur de l’attribut `version` lorsque vous réalisez une requête de recherche pour la destination. |

**Réponse**

La réponse inclut les détails mis à jour pour la destination, y compris son identifiant et la nouvelle `version` de la destination.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Suppression d’une destination

Si votre organisation n’a plus besoin d’une destination de projection, celle-ci peut-être supprimée en exécutant une requête DELETE au point de terminaison `/config/destinations` et en incluant l’identifiant de la destination que vous souhaitez supprimer dans le chemin d’accès de la requête.

>[!CAUTION]
>
>La réponse de l’API à la demande de suppression est immédiate, c’est pourquoi les modifications actuelles sur les données en périphérie se produisent de manière asynchrone. En d’autres termes, les données de profil seront retirées de toutes les périphéries (les `dataCenters` précisés dans la destination de projection), mais terminer le processus prendra du temps.

**Format d’API**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | L’ID unique de la destination de projection que vous souhaitez supprimer. |


**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La requête de suppression renvoie un état HTTP 204 (Pas de contenu) et un corps de réponse vide. Vous pouvez confirmer la réussite de la suppression en effectuant une requête de recherche pour la destination en utilisant son identifiant. La recherche doit renvoyer un état HTTP 404 (Not Found).

## Configurations de projection

Les configurations de projection fournissent des informations concernant les données disponibles pour chaque périphérie. Plutôt que de projeter un complete [!DNL Experience Data Model] (XDM) vers la périphérie, une projection fournit uniquement des données ou des champs spécifiques du schéma. Votre organisation peut définir plus d’une configuration de projection pour chaque schéma XDM.

### Liste de toutes les configurations de projection

Vous pouvez lister toutes les configurations de projection créées pour votre organisation en effectuant une requête GET sur le point de terminaison `/config/projections`. Vous pouvez également ajouter des paramètres facultatifs au chemin d’accès de la requête pour accéder à des configurations de projection pour un schéma particulier ou rechercher une projection individuelle en fonction de son nom.

**Format d’API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Paramètre | Description |
|---|---|
| `{SCHEMA_NAME}` | Le nom de la classe schéma associée à la configuration de projection à laquelle vous souhaitez accéder. |
| `{PROJECTION_NAME}` | Le nom de la configuration de projection auquel vous souhaitez accéder. |

>[!NOTE]
>
>`schemaName` est requis lorsque vous utilisez le paramètre `name`, comme nom de configuration de projection unique dans le contexte d’une classe schéma.

**Requête**

La requête suivante répertorie toutes les configurations de projection associées à la variable [!DNL Experience Data Model] classe schéma, [!DNL XDM Individual Profile]. Pour plus d’informations sur XDM et son rôle dans [!DNL Platform], veuillez commencer par lire le [Présentation du système XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des configurations de projection dans l’attribut racine `_embedded`, contenu dans le tableau `projectionConfigs`. Si aucune configuration de projection n’a été définie pour votre organisation, le tableau `projectionConfigs` sera vide.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Création de configuration de projection

Vous pouvez créer (POST) une nouvelle configuration de projection qui définira les champs XDM disponibles en périphérie.

**Format d’API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Paramètre | Description |
|---|---|
| `{SCHEMA_NAME}` | Le nom de la classe schéma associée à la configuration de projection à laquelle vous souhaitez accéder. |

**Requête**

>[!NOTE]
>
>La requête du POST pour créer une configuration nécessite une `Content-Type` comme illustré ci-dessous. L’utilisation d’un en-tête `Content-Type` incorrect entraîne un état HTTP 415 (Unsupported Media Type).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Propriété | Description |
|---|---|
| `selector` | Chaîne contenant une liste des propriétés du schéma à répercuter sur les périphéries. Les bonnes pratiques de travail avec les sélecteurs sont disponibles dans la section [Sélecteurs](#selectors) de ce document. |
| `name` | Un nom explicite pour la nouvelle configuration de projection. |
| `destinationId` | L’identifiant de la destination de périphérique vers lequel les données seront projetées. |

**Réponse**

Une réponse réussie renvoie les détails de la configuration de projection que vous venez de créer.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Sélecteurs {#selectors}

Un sélecteur est une liste de noms de champ XDM séparés par des virgules. Dans une configuration de projection, le sélecteur désigne les propriétés à inclure dans les projections. Le format de la valeur de paramètre `selector` est vaguement défini sur une syntaxe XPath. La syntaxe prise en charge est résumée ci-dessous avec des exemples supplémentaires fournis pour référence.

### Syntaxe prise en charge

* Utilisez des virgules pour sélectionner plusieurs champs. N’utilisez pas d’espaces.
* Utilisez la notation par point pour sélectionner des champs imbriqués.
   * Par exemple, pour sélectionner un champ intitulé `field` imbriqué dans un champ intitulé `foo`, utilisez le sélecteur `foo.field`.
* Lorsque vous incluez un champ qui contient des sous-champs, tous les sous-champs sont également projetés par défaut. Toutefois, vous pouvez filtrer les sous-champs renvoyés à l’aide de parenthèses `"( )"`.
   * Par exemple, `addresses(type,city.country)` renvoie uniquement le type d’adresse et le pays dans lequel la ville de l’adresse est située pour chaque élément du tableau `addresses`.
   * L’exemple ci-dessus équivaut à `addresses.type,addresses.city.country`.

>[!NOTE]
>
>La notation par points et la notation entre parenthèses sont toutes les deux prises en charge pour référencer les sous-champs. Toutefois, la bonne pratique consiste à utiliser la notation par point, car celle-ci est plus concise et fournit une meilleure illustration de la hiérarchie des champs.

* Chaque champ d’un sélecteur est associé spécifiquement à la racine de la réponse.
   * Si les données sont une collection de ressources, la projection inclura un tableau des ressources.
   * Si les données sont une ressource unique, la projection inclura des champs associés à cette ressource.
   * Si le champ que vous avez sélectionné est un tableau (ou en fait partie), la projection inclura la partie sélectionnée de tous les éléments du tableau.

### Exemples de paramètres du sélecteur

Les exemples suivants affichent des paramètres d’exemple `selector`, suivis par les valeurs structurées qu’elles représentent.

**person.lastName**

Renvoie le sous-champ `lastName` de l’objet `person` de la ressource demandée.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**addresses**

Renvoie tous les éléments du tableau `addresses`, y compris tous les champs de chaque élément, mais pas les autres champs.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,addresses**

Renvoie le champ `person.lastName` et tous les éléments du tableau `addresses`.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**addresses.city**

Renvoie uniquement le champ city pour tous les éléments du tableau addresses.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>Lorsqu’un champ imbriqué est renvoyé, la projection inclut les objets parents imbriqués. Les champs parents n’incluent pas d’autres champs enfants sauf s’ils sont également sélectionnés de manière explicite.

**addresses(type,city)**

Renvoie uniquement les valeurs des champs `type` et `city` pour chaque élément du tableau `addresses`. Tous les autres sous-champs contenus dans chaque élément `addresses` sont exclus du filtre.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Étapes suivantes

Ce guide vous a présenté les étapes impliquées afin de configurer des projections et des destinations, y compris la manière dont formater correctement la variable `selector` . Vous pouvez désormais créer de nouvelles destinations de projection et des configurations spécifiques aux besoins de votre entreprise.
