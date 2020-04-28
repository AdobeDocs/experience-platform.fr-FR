---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur d’API  client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: bb7aad4de681316cc9f9fd1d9310695bd220adb1

---


# Destinations et projections Edge

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs  en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en permanence au fur et à mesure des changements. Adobe Experience Platform permet cet accès en temps réel aux données grâce à l’utilisation de ce que l’on appelle les contours. Un bord est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles qu’Adobe  et  Adobe Campaign utilisent des bords afin de fournir des expériences client personnalisées en temps réel. Les données sont acheminées vers un bord par une projection, avec une destination de projection définissant le bord auquel les données seront envoyées et une configuration de projection définissant les informations spécifiques qui seront rendues disponibles sur le bord. Ce guide fournit des instructions détaillées sur l’utilisation de l’API  client en temps réel pour travailler avec les projections de périmètre, y compris les destinations et les configurations.

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de  client en temps réel. Avant de poursuivre, veuillez consulter le guide [en temps réel du développeur de clients](getting-started.md). En particulier, la section [de](getting-started.md#getting-started) prise en main du guide du développeur de  de comprend des liens vers des sujets connexes, un guide pour lire les exemples d’appels d’API dans ce  d’et des informations importantes sur les en-têtes requis nécessaires pour effectuer des appels vers les API de plateforme d’expérience.

## Destinations de projection

Une projection peut être routée vers un ou plusieurs arêtes en spécifiant les emplacements où les données doivent être envoyées. Chaque destination de projection créée possède un ID unique qui est ensuite utilisé pour créer la configuration de projection.

### toutes les destinations

Vous pouvez les destinations de bord qui ont déjà été créées pour votre entreprise en envoyant une requête GET au `/config/destinations` point de fin.

**Format API**

```http
GET /config/destinations
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un `projectionDestinations` tableau avec les détails de chaque destination affichés sous la forme d’un objet individuel dans le tableau. Si aucune prévision n’a été configurée, le tableau `projectionDestinations` renvoie vide.

>[!NOTE]
>Cette réponse a été raccourcie pour l’espace et ne montre que deux destinations.

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
| `_links.self.href` | Au niveau supérieur, correspond au chemin utilisé pour effectuer la demande GET. Dans chaque objet de destination, ce chemin peut être utilisé dans une requête GET pour rechercher directement les détails d’une destination spécifique. |
| `id` | Dans chaque objet de destination, l’ `"id"` objet affiche l’identifiant unique généré par le système et en lecture seule pour la destination. Cet identifiant est utilisé lors du référencement d’une destination spécifique et lors de la création de configurations de projection. |

Pour plus d&#39;informations sur les attributs d&#39;une destination individuelle, consultez la section sur la [création d&#39;une destination](#create-a-destination) qui suit.

### Création d’une destination {#create-a-destination}

Si la destination dont vous avez besoin n’existe pas déjà, vous pouvez créer une destination de projection en exécutant une requête POST sur le `/config/destinations` point de fin.

**Format API**

```http
POST /config/destinations
```

**Requête**

La requête suivante crée une nouvelle destination de bord.

>[!NOTE]
>La requête POST pour créer une destination requiert un en-tête spécifique, comme illustré ci-dessous. `Content-Type` L’utilisation d’un `Content-Type` en-tête incorrect génère une erreur HTTP Status 415 (Type de support non pris en charge).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `type` **(Obligatoire)** | Type de destination à créer. La seule valeur acceptée, &quot;EDGE&quot;, crée une destination de bord. |
| `dataCenters` **(Obligatoire)** | Tableau de chaînes qui  les bords vers lesquels les projections doivent être routées. Peut contenir une ou plusieurs des valeurs suivantes : &quot;OR1&quot; - Ouest des États-Unis, &quot;VA5&quot; - Est des États-Unis, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obligatoire)** | Indique l’expiration de la projection. Plage de valeurs acceptée : 600 à 604800. Valeur par défaut : 3600. |
| `replicationPolicy` **(Obligatoire)** | Définit le comportement de la réplication des données du concentrateur aux bords.  Valeurs prises en charge : PROACTIF, RÉACTIF. Valeur par défaut : RÉACTIF. |

**Réponse**

Une réponse réussie renvoie les détails de la destination du bord nouvellement créé, y compris l’identifiant unique généré par le système en lecture seule (`id`).

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
| `self.href` | Ce chemin est utilisé pour rechercher (GET) directement la destination et peut également être utilisé pour mettre à jour (PUT) ou supprimer (DELETE) la destination. |
| `id` | ID unique généré par le système et en lecture seule pour la destination. Cet ID est utilisé pour référencer directement la destination et lors de la création de configurations de projection. |
| `version` | Cette valeur en lecture seule indique la version actuelle de la destination. Lorsqu’une destination est mise à jour, le numéro de version est incrémenté automatiquement. |

### d’une destination

Si vous connaissez l’ID unique d’une destination de projection, vous pouvez exécuter une requête de recherche pour ses détails. Pour ce faire, vous devez envoyer une requête GET au point de `/config/destinations` fin et inclure l’ID de la destination dans le chemin d’accès de la requête.

**Format API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | ID unique de la destination de projection que vous souhaitez . |

**Requête**

La requête suivante effectue une recherche (GET) pour la destination de l’ID fourni dans le chemin de requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet response affiche les détails de la destination de la projection. L’ `id` attribut doit correspondre à l’ID de la destination de projection fourni dans la requête.

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

### Mettre à jour une destination

Une destination existante peut être mise à jour en envoyant une requête PUT au point de `/config/destinations` fin et en incluant l’ID de la destination à mettre à jour dans le chemin de la requête. Cette opération consiste essentiellement à _réécrire_ la destination. Par conséquent, les mêmes attributs doivent être fournis dans le corps de la requête que ceux fournis lors de la création d’une destination.

>[!CAUTION]
>La réponse de l’API à la demande de mise à jour est immédiate ; toutefois, les modifications apportées aux projections sont appliquées de manière asynchrone. En d’autres termes, il existe une différence de temps entre le moment où la définition de destination est mise à jour et celui où elle est appliquée.

**Format API**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | ID unique de la destination de projection que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour la destination existante pour inclure un second emplacement (`dataCenters`).

>[!IMPORTANT]
>La requête PUT requiert un `Content-Type` en-tête spécifique, comme illustré ci-dessous. L’utilisation d’un `Content-Type` en-tête incorrect génère une erreur HTTP Status 415 (Type de support non pris en charge).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `currentVersion` | Version actuelle de la destination existante. Valeur de l’ `version` attribut lors de l’exécution d’une demande de recherche pour la destination. |

**Réponse**

La réponse inclut les détails mis à jour pour la destination, y compris son ID et la nouvelle `version` de la destination.

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

Si votre organisation n’a plus besoin d’une destination de projection, vous pouvez la supprimer en faisant une requête DELETE au point de `/config/destinations` fin et en incluant l’ID de la destination que vous souhaitez supprimer dans le chemin d’accès de la requête.

>[!CAUTION]
>La réponse de l’API à la demande de suppression est immédiate ; toutefois, les modifications réelles apportées aux données sur les bords se produisent de manière asynchrone. En d’autres termes, les données  du seront supprimées de tous les bords (le `dataCenters` spécifié dans la destination de la projection), mais le processus prendra du temps à se terminer.

**Format API**

```
DELETE /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | ID unique de la destination de projection que vous souhaitez supprimer. |


**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La requête de suppression renvoie l’état HTTP 204 (Aucun contenu) et un corps de réponse vide. Vous pouvez confirmer que la suppression a réussi en exécutant une demande de recherche pour la destination par son identifiant. La recherche doit renvoyer l’état HTTP 404 (introuvable).

## Configurations de projection

Les configurations de projection fournissent des informations sur les données qui doivent être disponibles sur chaque bord. Plutôt que de projeter un XDM (Experience Data Model) complet sur le bord, une projection ne fournit que des données spécifiques, ou champs, du . Votre entreprise peut définir plusieurs configurations de projection pour chaque  XDM.

###  toutes les configurations de projection

Vous pouvez toutes les configurations de projection créées pour votre organisation en envoyant une requête GET au point de `/config/projections` fin. Vous pouvez également ajouter des paramètres facultatifs au chemin de requête pour accéder aux configurations de projection pour un particulier ou rechercher une projection individuelle par son nom.

**Format API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Paramètre | Description |
|---|---|
| `{SCHEMA_NAME}` | Nom de la classe de  associée à la configuration de projection à laquelle vous souhaitez accéder. |
| `{PROJECTION_NAME}` | Nom de la configuration de projection à laquelle vous souhaitez accéder. |

>[!NOTE]
>`schemaName` est requise lors de l’utilisation du `name` paramètre, car un nom de configuration de projection est unique dans le contexte d’une classe de .

**Requête**

Le de requête suivant  toutes les configurations de projection associées à la classe  de modèle de données d’expérience, XDM Individuel . Pour plus d&#39;informations sur XDM et son rôle dans Platform, veuillez commencer par lire la présentation [du système](../../xdm/home.md)XDM.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un de configurations de projection dans l’ `_embedded` attribut racine, contenu dans le `projectionConfigs` tableau. Si aucune configuration de projection n&#39;a été effectuée pour votre organisation, la `projectionConfigs` baie sera vide.

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

### Création d’une configuration de projection

Vous pouvez créer (POST) une nouvelle configuration de projection qui dictera les champs XDM disponibles sur les bords.

**Format API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Paramètre | Description |
|---|---|
| `{SCHEMA_NAME}` | Nom de la classe de  associée à la configuration de projection à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Propriété | Description |
|---|---|
| `selector` | Chaîne contenant un de propriétés dans le  à répliquer sur les bords. Les bonnes pratiques relatives à l’utilisation des sélecteurs sont disponibles dans la section [Sélecteurs](#selectors) de ce  de. |
| `name` | Nom descriptif de la nouvelle configuration de projection. |
| `destinationId` | Identifiant de la destination du bord vers laquelle les données seront projetées. |

**Réponse**

Une réponse réussie renvoie les détails de la configuration de projection nouvellement créée.

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

## Selectors {#selectors}

Un sélecteur est un de noms de champs XDM séparés par des virgules. Dans une configuration de projection, le sélecteur désigne les propriétés à inclure dans les projections. Le format de la valeur du `selector` paramètre est vaguement basé sur la syntaxe XPath. La syntaxe prise en charge est résumée ci-dessous, avec des exemples supplémentaires fournis à titre de référence.

### Syntaxe prise en charge

* Utilisez des virgules pour sélectionner plusieurs champs. N’utilisez pas d’espaces.
* Utilisez la notation par point pour sélectionner des champs imbriqués.
   * Par exemple, pour sélectionner un champ nommé `field` qui est imbriqué dans un champ nommé `foo`, utilisez le sélecteur `foo.field`.
* Lorsque vous incluez un champ contenant des sous-champs, tous les sous-champs sont également projetés par défaut. Vous pouvez toutefois filtrer les sous-champs renvoyés à l’aide de parenthèses `"( )"`.
   * Par exemple, `addresses(type,city.country)` renvoie uniquement le type d’adresse et le pays dans lequel la ville d’adresse est située pour chaque `addresses` élément de tableau.
   * L’exemple ci-dessus est équivalent à `addresses.type,addresses.city.country`.

>[!NOTE]
>La notation par points et la notation entre parenthèses sont prises en charge pour référencer les sous-champs. Toutefois, il est recommandé d’utiliser la notation par points car elle est plus concise et fournit une meilleure illustration de la hiérarchie des champs.

* Chaque champ d’un sélecteur est spécifié par rapport à la racine de la réponse.
   * Si les données sont un ensemble de ressources, la projection inclura un ensemble de ressources.
   * Si les données sont une ressource unique, la projection inclut les champs relatifs à cette ressource.
   * Si le champ sélectionné est (ou fait partie d’un tableau), la projection inclut la partie sélectionnée de tous les éléments du tableau.

### Exemples du paramètre selector

Les exemples suivants montrent des exemples `selector` de paramètres, suivis des valeurs structurées qu’ils représentent.

**person.lastName**

Renvoie le `lastName` sous-champ de l’ `person` objet dans la ressource demandée.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**adresses**

Renvoie tous les éléments du `addresses` tableau, y compris tous les champs de chaque élément, mais aucun autre champ.

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

**person.lastName,adresses**

Renvoie le `person.lastName` champ et tous les éléments du `addresses` tableau.

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

**address.city**

Renvoie uniquement le champ de ville pour tous les éléments du tableau d’adresses.

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
>Lorsqu’un champ imbriqué est renvoyé, la projection inclut les objets parents encadrés. Les champs parents n’incluent aucun autre champ enfant, sauf s’ils sont également sélectionnés explicitement.

**address(type,city)**

Renvoie uniquement les valeurs des champs `type` et `city` pour chaque élément du `addresses` tableau. Tous les autres sous-champs contenus dans chaque `addresses` élément sont exclus du filtre.

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

Ce guide vous montre les étapes nécessaires pour configurer les projections et les destinations de bord, y compris la manière de formater correctement le `selector` paramètre. Vous pouvez désormais créer de nouvelles destinations et projections de périmètre spécifiques aux besoins de votre entreprise. Pour découvrir d’autres actions disponibles par le biais de l’API , consultez le guide [du développeur de l’API de de clients en temps](getting-started.md)réel.