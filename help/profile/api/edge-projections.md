---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d464a6b4abd843f5f8545bc3aa8000f379a86c6d
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 2%

---


# Configurations de projection Edge et points de terminaison de destination

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs canaux en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en continu au fur et à mesure des changements. L&#39;Adobe Experience Platform permet cet accès en temps réel aux données grâce à ce que l&#39;on appelle les contours. Un bord est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles que l’Adobe Target et l’Adobe Campaign utilisent des bords afin de fournir des expériences personnalisées aux clients en temps réel. Les données sont acheminées vers un bord par une projection, avec une destination de projection qui définit le bord auquel les données seront envoyées et une configuration de projection qui définit les informations spécifiques qui seront rendues disponibles sur le bord. Ce guide fournit des instructions détaillées sur l’utilisation de l’API Profil client en temps réel pour travailler avec les projections de périmètre, y compris les destinations et les configurations.

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de l’API [Profil client en temps](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)réel. Avant de continuer, consultez le guide [de](getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

>[!NOTE]
>Les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un `Content-Type` en-tête. Plusieurs `Content-Type` sont utilisés dans ce document. Veuillez prêter une attention particulière aux en-têtes des exemples d’appels afin de vous assurer que vous utilisez le bon format `Content-Type` pour chaque demande.

## Destinations des projections

Une projection peut être acheminée vers un ou plusieurs arêtes en spécifiant les emplacements où les données doivent être envoyées. Chaque destination de projection créée possède un identifiant unique qui est ensuite utilisé pour créer la configuration de projection.

### Liste de toutes les destinations

Vous pouvez liste les destinations de périphérie qui ont déjà été créées pour votre organisation en envoyant une demande GET au point de `/config/destinations` terminaison.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un `projectionDestinations` tableau avec les détails de chaque destination affichés sous la forme d&#39;un objet individuel dans le tableau. Si aucune projection n&#39;a été configurée, le tableau `projectionDestinations` renvoie vide.

>[!NOTE]
>Cette réponse a été raccourcie pour l&#39;espace et ne montre que deux destinations.

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
| `_links.self.href` | Au niveau supérieur, correspond au chemin utilisé pour effectuer la demande GET. Dans chaque objet de destination individuel, ce chemin peut être utilisé dans une requête GET pour rechercher directement les détails d&#39;une destination spécifique. |
| `id` | Dans chaque objet de destination, le `"id"` indique l’identifiant unique généré par le système et en lecture seule pour la destination. Cet identifiant est utilisé lors du référencement d&#39;une destination spécifique et lors de la création de configurations de projection. |

Pour plus d&#39;informations sur les attributs d&#39;une destination individuelle, consultez la section sur la [création d&#39;une destination](#create-a-destination) qui suit.

### Créer une destination {#create-a-destination}

Si la destination dont vous avez besoin n&#39;existe pas déjà, vous pouvez créer une destination de projection en envoyant une requête POST au point de `/config/destinations` terminaison.

**Format d’API**

```http
POST /config/destinations
```

**Requête**

La requête suivante crée une nouvelle destination de bord.

>[!NOTE]
>La requête POST pour créer une destination requiert un en-tête spécifique, comme illustré ci-dessous. `Content-Type` L’utilisation d’un en-tête incorrect génère une erreur HTTP Status 415 (Type de support non pris en charge). `Content-Type`

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
| `dataCenters` **(Obligatoire)** | Tableau de chaînes qui liste les arêtes vers lesquelles les projections doivent être routées. Peut contenir une ou plusieurs des valeurs suivantes : &quot;OR1&quot; - États-Unis occidentaux, &quot;VA5&quot; - États-Unis orientaux, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obligatoire)** | Spécifie l&#39;expiration de projection. Plage de valeurs acceptée : 600 à 604800. Valeur par défaut : 3600. |
| `replicationPolicy` **(Obligatoire)** | Définit le comportement de la réplication des données du hub aux bords.  Valeurs prises en charge : PROACTIVE, RÉACTIVE. Valeur par défaut : RÉACTIF. |

**Réponse**

Une réponse réussie renvoie les détails de la destination de bord nouvellement créée, y compris l&#39;identifiant unique généré par le système en lecture seule (`id`).

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
| `id` | ID unique généré par le système en lecture seule pour la destination. Cet ID est utilisé pour référencer directement la destination et lors de la création de configurations de projection. |
| `version` | Cette valeur en lecture seule affiche la version actuelle de la destination. Lorsqu’une destination est mise à jour, le numéro de version est incrémenté automatiquement. |

### Vue d’une destination

Si vous connaissez l&#39;identifiant unique d&#39;une destination de projection, vous pouvez exécuter une demande de recherche pour en vue les détails. Pour ce faire, vous devez envoyer une requête GET au point de `/config/destinations` terminaison et inclure l’ID de la destination dans le chemin d’accès à la requête.

**Format d’API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | ID unique de la destination de projection que vous souhaitez vue. |

**Requête**

La requête suivante effectue une recherche (GET) pour vue de la destination de l’identifiant fourni dans le chemin de la requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

L’objet response affiche les détails de la destination de projection. L’ `id` attribut doit correspondre à l’ID de la destination de projection fournie dans la demande.

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

Une destination existante peut être mise à jour en envoyant une requête PUT au point de `/config/destinations` terminaison et en incluant l’ID de la destination à mettre à jour dans le chemin de la requête. Cette opération consiste essentiellement à _réécrire_ la destination. Par conséquent, les mêmes attributs doivent être fournis dans le corps de la requête que ceux fournis lors de la création d’une nouvelle destination.

>[!CAUTION]
>La réponse de l’API à la demande de mise à jour est immédiate, mais les modifications apportées aux projections sont appliquées de manière asynchrone. En d&#39;autres termes, il y a une différence de temps entre le moment où la définition de destination est mise à jour et celui où elle est appliquée.

**Format d’API**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Paramètre | Description |
|---|---|
| `{DESTINATION_ID}` | ID unique de la destination de projection que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour la destination existante pour inclure un second emplacement (`dataCenters`).

>[!IMPORTANT]
>La requête PUT requiert un `Content-Type` en-tête spécifique, comme illustré ci-dessous. L’utilisation d’un en-tête incorrect génère une erreur HTTP Status 415 (Type de support non pris en charge). `Content-Type`

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

La réponse comprend les détails mis à jour pour la destination, y compris son identifiant et la nouvelle `version` de la destination.

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

Si votre organisation ne requiert plus de destination de projection, elle peut être supprimée en adressant une requête de DELETE au point de `/config/destinations` terminaison et en incluant l&#39;ID de la destination que vous souhaitez supprimer dans le chemin de la demande.

>[!CAUTION]
>La réponse de l’API à la demande de suppression est immédiate, mais les modifications réelles apportées aux données sur les bords se produisent de manière asynchrone. En d&#39;autres termes, les données du profil seront supprimées de toutes les arêtes (les `dataCenters` données spécifiées dans la destination de la projection), mais le processus prendra du temps.

**Format d’API**

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

La demande de suppression renvoie l’état HTTP 204 (Aucun contenu) et un corps de réponse vide. Vous pouvez confirmer que la suppression a réussi en exécutant une demande de recherche pour la destination par son identifiant. La recherche doit renvoyer l&#39;état HTTP 404 (introuvable).

## Configurations de projection

Les configurations de projection fournissent des informations sur les données qui doivent être disponibles sur chaque bord. Plutôt que de projeter un schéma XDM (Experience Data Model) complet sur le bord, une projection ne fournit que des données spécifiques, ou champs, du schéma. Votre entreprise peut définir plusieurs configurations de projection pour chaque schéma XDM.

### Liste de toutes les configurations de projection

Vous pouvez liste toutes les configurations de projection qui ont été créées pour votre organisation en envoyant une requête GET au point de `/config/projections` terminaison. Vous pouvez également ajouter des paramètres facultatifs au chemin de requête pour accéder aux configurations de projection pour un schéma particulier ou rechercher une projection individuelle par son nom.

**Format d’API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Paramètre | Description |
|---|---|
| `{SCHEMA_NAME}` | Nom de la classe de schéma associée à la configuration de projection à laquelle vous souhaitez accéder. |
| `{PROJECTION_NAME}` | Nom de la configuration de projection à laquelle vous souhaitez accéder. |

>[!NOTE]
>`schemaName` est requis lors de l&#39;utilisation du `name` paramètre, car un nom de configuration de projection n&#39;est unique que dans le contexte d&#39;une classe de schéma.

**Requête**

La demande suivante liste toutes les configurations de projection associées à la classe de schéma de modèle de données d’expérience, Profil XDM individuel. Pour plus d&#39;informations sur XDM et son rôle dans Platform, veuillez commencer par lire la présentation [du système](../../xdm/home.md)XDM.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de configurations de projection dans l&#39;attribut `_embedded` racine, contenu dans le `projectionConfigs` tableau. Si aucune configuration de projection n&#39;a été effectuée pour votre organisation, la `projectionConfigs` baie sera vide.

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

### Créer une configuration de projection

Vous pouvez créer (POST) une nouvelle configuration de projection qui dictera les champs XDM disponibles sur les bords.

**Format d’API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Paramètre | Description |
|---|---|
| `{SCHEMA_NAME}` | Nom de la classe de schéma associée à la configuration de projection à laquelle vous souhaitez accéder. |

**Requête**

>[!NOTE]
>La demande POST pour créer une configuration requiert un en-tête spécifique, comme illustré ci-dessous. `Content-Type` L’utilisation d’un en-tête incorrect génère une erreur HTTP Status 415 (Type de support non pris en charge). `Content-Type`

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `selector` | Chaîne contenant une liste de propriétés dans le schéma à répliquer sur les bords. Les bonnes pratiques relatives à l’utilisation des sélecteurs sont disponibles dans la section [Sélecteurs](#selectors) de ce document. |
| `name` | Nom descriptif de la nouvelle configuration de projection. |
| `destinationId` | Identifiant de la destination de bord vers laquelle les données seront projetées. |

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

Un sélecteur est une liste de noms de champs XDM séparés par des virgules. Dans une configuration de projection, le sélecteur désigne les propriétés à inclure dans les projections. Le format de la valeur du `selector` paramètre est approximativement basé sur la syntaxe XPath. La syntaxe prise en charge est résumée ci-dessous, avec des exemples supplémentaires fournis à titre de référence.

### Syntaxe prise en charge

* Utilisez des virgules pour sélectionner plusieurs champs. N’utilisez pas d’espaces.
* Utilisez la notation par point pour sélectionner les champs imbriqués.
   * Par exemple, pour sélectionner un champ nommé `field` qui est imbriqué dans un champ nommé `foo`, utilisez le sélecteur `foo.field`.
* Lors de l’inclusion d’un champ contenant des sous-champs, tous les sous-champs sont également projetés par défaut. Vous pouvez toutefois filtrer les sous-champs renvoyés à l’aide de parenthèses `"( )"`.
   * Par exemple, `addresses(type,city.country)` renvoie uniquement le type d&#39;adresse et le pays dans lequel la ville d&#39;adresse est située pour chaque élément de `addresses` tableau.
   * L&#39;exemple ci-dessus est équivalent à `addresses.type,addresses.city.country`.

>[!NOTE]
>La notation par points et la notation entre parenthèses sont prises en charge pour référencer les sous-champs. Cependant, il est recommandé d’utiliser la notation par point car elle est plus concise et fournit une meilleure illustration de la hiérarchie des champs.

* Chaque champ d’un sélecteur est spécifié par rapport à la racine de la réponse.
   * Si les données sont un ensemble de ressources, la projection inclura un ensemble de ressources.
   * Si les données sont une ressource unique, la projection inclut les champs relatifs à cette ressource.
   * Si le champ sélectionné est (ou fait partie d&#39;un tableau), la projection inclut la partie sélectionnée de tous les éléments du tableau.

### Exemples du paramètre de sélecteur

Les exemples suivants montrent des exemples `selector` de paramètres, suivis des valeurs structurées qu’ils représentent.

**person.lastName**

Renvoie le `lastName` sous-champ de l&#39; `person` objet dans la ressource demandée.

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

Renvoie uniquement le champ de ville pour tous les éléments du tableau d&#39;adresses.

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

Ce guide vous montre les étapes nécessaires à la configuration des projections et des destinations, y compris la manière de formater correctement le `selector` paramètre. Vous pouvez désormais créer de nouvelles destinations de projection et de nouvelles configurations spécifiques aux besoins de votre entreprise.