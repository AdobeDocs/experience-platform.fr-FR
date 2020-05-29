---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 9600f315f162b6cd86e2dbe2fffc793cc91c9319
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---


# Entités (accès au Profil)

La plateforme Adobe Experience Platform vous permet d’accéder aux données du Profil client en temps réel à l’aide des API RESTful ou de l’interface utilisateur. Ce guide décrit comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l’aide de l’API. Pour plus d&#39;informations sur l&#39;accès aux données de Profil à l&#39;aide de l&#39;interface utilisateur de la plate-forme, consultez le guide [d&#39;utilisation du](../ui/user-guide.md)Profil.

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API Profil client en temps réel. Avant de continuer, consultez le guide [du développeur de l’API Profil client en temps](getting-started.md)réel.

En particulier, la section [](getting-started.md#getting-started) Prise en main du guide du développeur de Profils contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Accès aux données du profil par identité

Vous pouvez accéder à une entité de Profil en adressant une requête GET au point de `/access/entities` terminaison et en fournissant l’identité de l’entité sous la forme d’une série de paramètres de requête. Cette identité se compose d&#39;une valeur d&#39;identifiant (`entityId`) et de l&#39;espace de nommage d&#39;identité (`entityIdNS`).

Les paramètres de Requête fournis dans le chemin d’accès à la requête spécifient les données à accéder. Vous pouvez inclure plusieurs paramètres, séparés par des esperluettes (&amp;). Une liste complète des paramètres valides est fournie dans la section des paramètres [de](#query-parameters) requête de l&#39;appendice.

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Requête**

La requête suivante récupère le courrier électronique et le nom d’un client à l’aide d’une identité :

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

>[!NOTE]
>Si un graphique associé lie plus de 50 identités, ce service renvoie l’état HTTP 422 et le message &quot;Trop d’identités liées&quot;. Si vous recevez cette erreur, pensez à ajouter d&#39;autres paramètres de requête pour restreindre votre recherche.

## Accès aux données du profil par liste d&#39;identités

Vous pouvez accéder à plusieurs entités de profil en fonction de leur identité en adressant une requête POST au point de `/access/entities` terminaison et en fournissant les identités dans la charge utile. Ces identités se composent d’une valeur d’identification (`entityId`) et d’un espace de nommage d’identité (`entityIdNS`).

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les noms et adresses électroniques de plusieurs clients par une liste d’identités :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Propriété | Description |
|---|---|
| `schema.name` | ***(Obligatoire)*** Nom du schéma XDM auquel appartient l&#39;entité. |
| `fields` | Champs XDM à renvoyer, sous forme de tableau de chaînes. Par défaut, tous les champs sont renvoyés. |
| `identities` | ***(Obligatoire)*** Tableau contenant une liste d&#39;identités pour les entités auxquelles vous voulez accéder. |
| `identities.entityId` | ID d&#39;une entité à laquelle vous souhaitez accéder. |
| `identities.entityIdNS.code` | espace de nommage d’un ID d’entité auquel vous souhaitez accéder. |
| `timeFilter.startTime` | Heure de Début du filtre de période, incluse. Doit être à la granularité de millisecondes. Si elle n’est pas spécifiée, la valeur par défaut est le début de l’heure disponible. |
| `timeFilter.endTime` | Filtre de la période de fin, exclu. Doit être à la granularité de millisecondes. Si elle n’est pas spécifiée, la valeur par défaut est la fin de l’heure disponible. |
| `limit` | Nombre d&#39;enregistrements à renvoyer. S’applique uniquement au nombre de événements d’expérience renvoyés. Par défaut : 1000. |
| `orderby` | Ordre de tri des événements d’expérience récupérés par horodatage, écrit comme `(+/-)timestamp` par défaut `+timestamp`. |
| `withCA` | Indicateur de fonction permettant d’activer les attributs calculés pour la recherche. Par défaut : false. |

**Réponse** Une réponse positive renvoie les champs demandés des entités spécifiés dans le corps de la demande.

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Accès aux événements de séries chronologiques pour un profil par identité

Vous pouvez accéder aux événements de séries chronologiques en fonction de l’identité de l’entité de profil associée en adressant une demande GET au point de `/access/entities` terminaison. Cette identité se compose d&#39;une valeur d&#39;identifiant (`entityId`) et d&#39;un espace de nommage d&#39;identité (`entityIdNS`).

Les paramètres de Requête fournis dans le chemin d’accès à la requête spécifient les données à accéder. Vous pouvez inclure plusieurs paramètres, séparés par des esperluettes (&amp;). Une liste complète des paramètres valides est fournie dans la section des paramètres [de](#query-parameters) requête de l&#39;appendice.

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Requête**

La requête suivante recherche une entité de profil par ID et récupère les valeurs des propriétés `endUserIDs`, `web`et `channel` pour tous les événements de séries chronologiques associés à l&#39;entité.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste paginée de événements de série chronologique et de champs associés spécifiés dans les paramètres de requête de la demande.

>[!NOTE]
>La requête spécifiait une limite de un (`limit=1`), par conséquent la `count` réponse ci-dessous est 1 et une seule entité est renvoyée.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Accéder à une page de résultats suivante

Les résultats sont paginés lors de la récupération de événements de séries chronologiques. S’il y a des pages de résultats suivantes, la `_page.next` propriété contient un identifiant. En outre, la `_links.next.href` propriété fournit un URI de demande pour récupérer la page suivante. Pour récupérer les résultats, effectuez une autre requête GET sur le `/access/entities` point de terminaison, mais vous devez être sûr de remplacer `/entities` par la valeur de l’URI fourni.

>[!NOTE]
>Veillez à ne pas répéter accidentellement `/entities/` le chemin d’accès à la requête. Il ne doit apparaître qu&#39;une seule fois comme : `/access/entities?start=...`

**Format d’API**

```http
GET /access/{NEXT_URI}
```

| Paramètre | Description |
|---|---|
| `{NEXT_URI}` | Valeur URI provenant de `_links.next.href`. |

**Requête**

La requête suivante récupère la page de résultats suivante en utilisant l’ `_links.next.href` URI comme chemin de requête.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la page suivante des résultats. Cette réponse ne comporte pas de pages de résultats ultérieures, comme indiqué par les valeurs de chaîne vides de `_page.next` et `_links.next.href`.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Accéder aux événements de séries chronologiques pour plusieurs profils par identité

Vous pouvez accéder aux événements de séries chronologiques à partir de plusieurs profils associés en adressant une requête POST au point de `/access/entities` terminaison et en fournissant les identités de profil dans la charge utile. Ces identités se composent chacune d’une valeur d’identification (`entityId`) et d’un espace de nommage d’identité (`entityIdNS`).

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les ID utilisateur, les heures locales et les codes de pays pour les événements de séries chronologiques associés à une liste d’identités de profil :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| Propriété | Description |
|---|---|
| `schema.name` | **(OBLIGATOIRE)** schéma XDM de l&#39;entité à récupérer |
| `relatedSchema.name` | Si `schema.name` cette valeur `_xdm.context.experienceevent` est définie, elle doit indiquer le schéma de l&#39;entité de profil à laquelle les événements de séries chronologiques sont liés. |
| `identities` | **(OBLIGATOIRE)** Tableau répertoriant les profils à partir desquels récupérer les événements de séries chronologiques associés. Chaque entrée du tableau est définie de deux manières : 1) en utilisant une identité complète composée de la valeur d’ID et de l’espace de nommage ou 2) en fournissant un XID. |
| `fields` | Isole les données renvoyées à un ensemble de champs spécifié. Utilisez cette option pour filtrer quels champs de schéma sont inclus dans les données récupérées. Exemple : personalEmail,person.name,person.gender |
| `mergePolicyId` | Identifie la stratégie de fusion selon laquelle gérer les données renvoyées. Si l’un d’eux n’est pas spécifié dans l’appel de service, la valeur par défaut de votre organisation pour ce schéma est utilisée. Si aucune stratégie de fusion par défaut n’a été configurée, la valeur par défaut est l’absence de fusion de profil et d’assemblage d’identité. |
| `orderby` | Ordre de tri des événements d’expérience récupérés par horodatage, écrit comme `(+/-)timestamp` par défaut `+timestamp`. |
| `timeFilter.startTime` | Spécifiez l’heure de début de filtrage des objets de série chronologique (en millisecondes). |
| `timeFilter.endTime` | Spécifiez l’heure de fin pour filtrer les objets de série chronologique (en millisecondes). |
| `limit` | Valeur numérique indiquant le nombre maximal d’objets à renvoyer. Par défaut : 1 000 |
| `withCA` | Indicateur de fonction permettant d’activer les attributs calculés pour la recherche. Par défaut : false |

**Réponse**

Une réponse réussie renvoie une liste paginée de événements de séries chronologiques associés aux plusieurs profils spécifiés dans la demande.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

Dans cet exemple de réponse, le premier profil répertorié (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) fournit une valeur pour `_links.next.payload`, ce qui signifie qu’il y a des pages de résultats supplémentaires pour ce profil. Consultez la section suivante sur l&#39; [accès aux résultats](#access-additional-results) supplémentaires pour en savoir plus sur la façon d&#39;accéder à ces résultats supplémentaires.

### Accès à d’autres résultats {#access-additional-results}

Lors de la récupération des événements de séries chronologiques, il peut y avoir de nombreux résultats renvoyés, de sorte que les résultats sont souvent paginés. S’il existe des pages de résultats suivantes pour un profil particulier, la `_links.next.payload` valeur de ce profil contiendra un objet de charge utile.

En utilisant cette charge dans le corps de la requête, vous pouvez exécuter une requête POST supplémentaire sur le `access/entities` point de terminaison pour récupérer la page suivante des données de séries chronologiques pour ce profil.

## Accéder aux événements de séries chronologiques dans plusieurs entités de schéma

Vous pouvez accéder à plusieurs entités connectées par le biais d’un descripteur de relation. L&#39;exemple d&#39;appel d&#39;API suivant suppose qu&#39;une relation a déjà été définie entre deux schémas. Pour plus d&#39;informations sur les descripteurs de relation, veuillez lire le sous-guide [](../../xdm/api/descriptors.md)descripteurs du guide du développeur de l&#39;API de registre de Schéma.

Vous pouvez inclure des paramètres de requête dans le chemin d’accès à la requête afin de spécifier les données à accéder. Vous pouvez inclure plusieurs paramètres, séparés par des esperluettes (&amp;). Une liste complète des paramètres valides est fournie dans la section des paramètres [de](#query-parameters) requête de l&#39;appendice.

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Requête**

La requête suivante récupère une entité contenant un descripteur de relation précédemment établi pour accéder à des informations sur différents schémas.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie une liste paginée de événements de séries chronologiques associés aux différentes entités.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Accéder à une page de résultats suivante

Les résultats sont paginés lors de la récupération de événements de séries chronologiques. S’il y a des pages de résultats suivantes, la `_page.next` propriété contient un identifiant. En outre, la `_links.next.href` propriété fournit un URI de requête pour récupérer la page suivante en envoyant des requêtes GET supplémentaires au `access/entities` point de terminaison.

## Étapes suivantes

En suivant ce guide, vous avez réussi à accéder aux champs de données du Profil client en temps réel, aux profils et aux données de séries chronologiques. Pour savoir comment accéder à d&#39;autres ressources de données stockées dans la plate-forme, consultez l&#39;aperçu [de l&#39;accès aux](../../data-access/home.md)données.

## Annexe {#appendix}

La section suivante fournit des informations supplémentaires sur l’accès aux données de Profil à l’aide de l’API.

### Paramètres de Requête {#query-parameters}

Les paramètres suivants sont utilisés dans le chemin d’accès des requêtes GET au point de `/access/entities` terminaison. Ils permettent d&#39;identifier l&#39;entité de profil à laquelle vous souhaitez accéder et de filtrer les données renvoyées dans la réponse. Les paramètres requis sont marqués, tandis que les autres sont facultatifs.

| Paramètre | Description | Exemple |
|---|---|---|
| `schema.name` | **(OBLIGATOIRE)** schéma XDM de l&#39;entité à récupérer | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Si `schema.name` est &quot;_xdm.context.experience.event&quot;, cette valeur doit spécifier le schéma de l’entité de profil à laquelle les événements de séries chronologiques sont liés. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBLIGATOIRE)** ID de l’entité. Si la valeur de ce paramètre n’est pas un XID, un paramètre d’espace de nommage d’identité doit également être fourni (voir `entityIdNS` ci-dessous). | `entityId=janedoe@example.com` |
| `entityIdNS` | Si `entityId` ce champ n’est pas fourni en tant que XID, il doit spécifier l’espace de nommage d’identité. | `entityIdNE=email` |
| `relatedEntityId` | Si `schema.name` est &quot;_xdm.context.experience.event&quot;, cette valeur doit spécifier l’espace de nommage d’identité de l’entité de profil associée. Cette valeur suit les mêmes règles que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Si `schema.name` est &quot;_xdm.context.experience.event&quot;, cette valeur doit spécifier l’espace de nommage d’identité pour l’entité spécifiée dans `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtres les données renvoyées dans la réponse. Utilisez cette option pour spécifier les valeurs de champ de schéma à inclure dans les données récupérées. Pour plusieurs champs, séparez les valeurs par une virgule sans espaces entre | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifie la stratégie de fusion selon laquelle gérer les données renvoyées. Si l’un d’eux n’est pas spécifié dans l’appel, la valeur par défaut de votre organisation pour ce schéma est utilisée. Si aucune stratégie de fusion par défaut n’a été configurée, la valeur par défaut est l’absence de fusion de profil et d’assemblage d’identité. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Ordre de tri des événements d’expérience récupérés par horodatage, écrit comme `(+/-)timestamp` par défaut `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Spécifiez l’heure de début de filtrage des objets de série chronologique (en millisecondes). | `startTime=1539838505` |
| `endTime` | Spécifiez l’heure de fin pour filtrer les objets de série chronologique (en millisecondes). | `endTime=1539838510` |
| `limit` | Valeur numérique indiquant le nombre maximal d’objets à renvoyer. Par défaut : 1 000 | `limit=100` |
| `withCA` | Indicateur de fonction permettant d’activer les attributs calculés pour la recherche. Par défaut : false | `withCA=true` |