---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API Entités (accès au profil)
type: Documentation
description: Adobe Experience Platform vous permet d’accéder aux données de Real-time Customer Profile à l’aide des API RESTful ou de l’interface utilisateur. Ce guide explique comment accéder aux entités, plus communément appelées "profils", à l’aide de l’API Profile.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 89%

---

# Point de terminaison des entités (accès au profil)

Adobe Experience Platform vous permet d&#39;accéder aux données [!DNL Real-Time Customer Profile] à l&#39;aide des API RESTful ou de l&#39;interface utilisateur. Ce guide explique comment accéder aux entités, plus communément appelées « profils », à l’aide de l’API. Pour plus d’informations sur l’accès aux profils à l’aide de l’interface utilisateur [!DNL Platform], reportez-vous au [guide d’utilisation du profil](../ui/user-guide.md).

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Accès aux données de profil par identité

Vous pouvez accéder à une entité [!DNL Profile] en effectuant une requête de GET sur le point de terminaison `/access/entities` et en fournissant l’identité de l’entité sous la forme d’une série de paramètres de requête. Cette identité se compose d’une valeur d’identifiant (`entityId`) et de l’espace de noms d’identité (`entityIdNS`).

Les paramètres de requête fournis dans le chemin de la requête spécifient les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres, séparés par des esperluettes (&amp;). Une liste complète de paramètres valides est fournie dans la section des [paramètres de requête](#query-parameters) de l’annexe.

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Requête**

La requête suivante récupère l’adresse e-mail et le nom d’un client à l’aide d’une identité :

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>
>Si un graphique associé lie plus de 50 identités, ce service renvoie un état HTTP 422 et le message « Trop d’identités connexes ». Si cette erreur s’affiche, pensez à ajouter d’autres paramètres de requête pour affiner votre recherche.

## Accès aux données de profil par liste d’identités

Vous pouvez accéder à plusieurs entités de profil grâce à leur identité en effectuant une requête POST sur le point d’entrée `/access/entities` et en fournissant les identités dans le payload. Ces identités se composent d’une valeur d’identifiant (`entityId`) et d’un espace de noms d’identité (`entityIdNS`).

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les noms et adresses électroniques de plusieurs clients à l’aide d’une liste d’identités :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schema.name` | ***(Obligatoire)*** Le nom du schéma XDM auquel appartient l’entité. |
| `fields` | Les champs XDM à renvoyer, sous forme de tableau de chaînes. Tous les champs sont renvoyés par défaut. |
| `identities` | ***(Obligatoire)*** Un tableau contenant une liste d’identités pour les entités auxquelles vous souhaitez accéder. |
| `identities.entityId` | L’identifiant d’une entité à laquelle vous souhaitez accéder. |
| `identities.entityIdNS.code` | L’espace de noms d’un identifiant d’entité auquel vous souhaitez accéder. |
| `timeFilter.startTime` | L’heure de début du filtre d’intervalle de temps, incluse. La granularité doit être exprimée en millisecondes. Si elle n’est pas spécifiée, la valeur par défaut est le début de l’heure disponible. |
| `timeFilter.endTime` | L’heure de fin du filtre d’intervalle de temps, exclue. La granularité doit être exprimée en millisecondes. Si elle n’est pas spécifiée, la valeur par défaut est la fin de l’heure disponible. |
| `limit` | Nombre d’enregistrements à renvoyer. S’applique uniquement au nombre d’événements d’expérience renvoyés. Valeur par défaut : 1 000. |
| `orderby` | L’ordre de tri des événements d’expérience récupérés par date et heure, indiqué par `(+/-)timestamp`, la valeur par défaut étant `+timestamp`. |
| `withCA` | Indicateur de fonction permettant d’activer les attributs calculés pour la recherche. Valeur par défaut : false. |

**Réponse**
Une réponse réussie renvoie les champs requis des entités spécifiées dans le corps de la requête.

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

## Accès aux événements de série temporelle d’un profil par identité

Vous pouvez accéder aux événements de série temporelle à l’aide de l’identité de leur entité de profil connexe en effectuant une requête GET sur le point d’entrée `/access/entities`. Cette identité se compose d’une valeur d’identifiant (`entityId`) et d’un espace de noms d’identité (`entityIdNS`).

Les paramètres de requête fournis dans le chemin de la requête spécifient les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres, séparés par des esperluettes (&amp;). Une liste complète de paramètres valides est fournie dans la section des [paramètres de requête](#query-parameters) de l’annexe.

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Requête**

La requête suivante recherche une entité de profil à l’aide de l’identifiant et récupère les valeurs des propriétés `endUserIDs`, `web` et `channel` pour tous les événements de série temporelle associés à l’entité.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste paginée d’événements de série temporelle et des champs associés spécifiés dans les paramètres de requête.

>[!NOTE]
>
>La requête spécifie une limite de un (`limit=1`), donc le `count` de la réponse ci-dessous est de 1 et une seule entité est renvoyée.

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

### Accès à une page de résultats ultérieure

Les résultats sont paginés lors de la récupération des événements de série temporelle. Si des pages de résultats ultérieures sont disponibles, la propriété `_page.next` contiendra un identifiant. En outre, la propriété `_links.next.href` fournit un URI de requête pour récupérer la page suivante. Pour récupérer les résultats, effectuez une autre requête GET sur le point d’entrée `/access/entities`, mais assurez-vous de remplacer `/entities` par la valeur de l’URI fourni.

>[!NOTE]
>
>Veillez à ne pas répéter accidentellement `/entities/` dans le chemin de requête. Il ne doit apparaître qu’une seule fois, par exemple : `/access/entities?start=...`

**Format d’API**

```http
GET /access/{NEXT_URI}
```

| Paramètre | Description |
|---|---|
| `{NEXT_URI}` | La valeur URI provenant de `_links.next.href`. |

**Requête**

La requête suivante récupère la page de résultats suivante en utilisant l’URI `_links.next.href` comme chemin de requête.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la page de résultats suivante. Cette réponse ne comporte pas de pages de résultats ultérieures, comme indiqué par les valeurs de chaîne vides de `_page.next` et `_links.next.href`.

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

## Accès aux événements de série temporelle de plusieurs profils par identités

Vous pouvez accéder aux événements de série temporelle de plusieurs profils connexes en effectuant une requête POST sur le point d’entrée `/access/entities` et en fournissant les identités de profil du payload. Chaque identité se compose d’une valeur d’identifiant (`entityId`) et d’un espace de noms d’identité (`entityIdNS`).

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les identifiants d’utilisateur, les heures locales et les codes pays pour les événements de série temporelle associés à une liste d’identités de profil :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schema.name` | **(OBLIGATOIRE)** Le schéma XDM de l’entité à récupérer |
| `relatedSchema.name` | Si `schema.name` correspond à `_xdm.context.experienceevent`, cette valeur doit spécifier le schéma de l’entité de profil à laquelle les événements de série temporelle sont associés. |
| `identities` | **(OBLIGATOIRE)** Un tableau répertoriant les profils pour récupérer les événements de série temporelle associés. Chaque entrée du tableau est définie de l’une des deux façons suivantes : 1) en utilisant une identité complète composée d’une valeur d’identifiant et d’un espace de noms ou 2) en fournissant un XID. |
| `fields` | Isole les données renvoyées à un ensemble de champs spécifié. Utilisez cette option pour filtrer les champs de schéma inclus dans les données récupérées. Exemple : personalEmail,person.name,person.gender |
| `mergePolicyId` | Identifie la politique de fusion qui doit régir les données renvoyées. Si l’un d’eux n’est pas spécifié dans l’appel de service, la valeur par défaut de votre organisation pour ce schéma sera utilisée. Si aucune politique de fusion par défaut n’a été configurée, la valeur par défaut est l’absence de fusion de profils et de combinaison d’identités. |
| `orderby` | L’ordre de tri des événements d’expérience récupérés par date et heure, indiqué par `(+/-)timestamp`, la valeur par défaut étant `+timestamp`. |
| `timeFilter.startTime` | Spécifiez l’heure de début pour filtrer les objets de série temporelle (en millisecondes). |
| `timeFilter.endTime` | Spécifiez l’heure de fin pour filtrer les objets de série temporelle (en millisecondes). |
| `limit` | Valeur numérique spécifiant le nombre maximal d’objets à renvoyer. Valeur par défaut : 1000 |
| `withCA` | Indicateur de fonction permettant d’activer les attributs calculés pour la recherche. Valeur par défaut : false |

**Réponse**

Une réponse réussie renvoie une liste paginée d’événements de série temporelle associés aux multiples profils spécifiés dans la requête.

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

Dans cet exemple de réponse, le premier profil répertorié (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) fournit une valeur pour `_links.next.payload`, ce qui signifie que des pages de résultats supplémentaires sont disponibles pour ce profil. Consultez la section suivante sur l’[accès aux résultats supplémentaires](#access-additional-results) pour savoir comment accéder à ces résultats supplémentaires.

### Accès aux résultats supplémentaires {#access-additional-results}

Lors de la récupération d’événements de série temporelle, il se peut que de nombreux résultats soient renvoyés. Par conséquent, les résultats sont souvent paginés. Si un profil particulier comporte des pages de résultats ultérieures, la valeur `_links.next.payload` de ce profil contiendra un objet de payload.

En utilisant ce payload dans le corps de la requête, vous pouvez effectuer une requête POST supplémentaire sur le point d’entrée `access/entities` pour récupérer la page ultérieure des données de série temporelle pour ce profil.

## Accès aux événements de série temporelle dans plusieurs entités de schéma

Vous pouvez accéder à plusieurs entités connectées par le biais d’un descripteur de relation. L’exemple d’appel API suivant part du principe qu’une relation a déjà été définie entre deux schémas. Pour plus d’informations sur les descripteurs de relation, consultez le [!DNL Schema Registry] guide de développement de l’API [guide de point de terminaison des descripteurs](../../xdm/api/descriptors.md).

Vous pouvez inclure des paramètres de requête dans le chemin de la requête afin de spécifier les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres, séparés par des esperluettes (&amp;). Une liste complète de paramètres valides est fournie dans la section des [paramètres de requête](#query-parameters) de l’annexe.

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Requête**

La requête suivante récupère une entité contenant un descripteur de relation préalablement établi afin d’accéder aux informations sur différents schémas.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une réponse réussie renvoie une liste paginée d’événements de série temporelle associés aux multiples entités.

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

### Accès à une page de résultats ultérieure

Les résultats sont paginés lors de la récupération des événements de série temporelle. Si des pages de résultats ultérieures sont disponibles, la propriété `_page.next` contiendra un identifiant. De plus, la propriété `_links.next.href` fournit un URI de requête pour récupérer la page ultérieure en effectuant des requêtes GET supplémentaires sur le point d’entrée `access/entities`.

## Étapes suivantes

En suivant ce guide, vous avez réussi à accéder aux [!DNL Real-Time Customer Profile] champs de données, profils et données de série temporelle. Pour savoir comment accéder à d’autres ressources de données stockées dans [!DNL Platform], consultez la [présentation de l’accès aux données](../../data-access/home.md).

## Annexe {#appendix}

La section suivante fournit des informations supplémentaires sur l’accès aux données [!DNL Profile] à l’aide de l’API.

### Paramètres de requête {#query-parameters}

Les paramètres suivants sont utilisés dans le chemin des requêtes GET vers le point d’entrée `/access/entities`. Ils permettent d’identifier l’entité de profil à laquelle vous souhaitez accéder et de filtrer les données renvoyées dans la réponse. Les paramètres requis sont signalés par un libellé, tandis que les autres sont facultatifs.

| Paramètre | Description | Exemple |
|---|---|---|
| `schema.name` | **(OBLIGATOIRE)** Le schéma XDM de l’entité à récupérer | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Si `schema.name` correspond à &quot;_xdm.context.experienceevent&quot;, cette valeur doit spécifier le schéma de l’entité de profil à laquelle les événements de série temporelle sont liés. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBLIGATOIRE)** L’identifiant de l’entité. Si la valeur de ce paramètre n’est pas un XID, un paramètre d’espace de noms d’identité doit également être fourni (voir `entityIdNS` ci-dessous). | `entityId=janedoe@example.com` |
| `entityIdNS` | Si `entityId` n’est pas fourni en tant que XID, ce champ doit spécifier l’espace de noms d’identité. | `entityIdNE=email` |
| `relatedEntityId` | Si `schema.name` correspond à &quot;_xdm.context.experienceevent&quot;, cette valeur doit spécifier l’espace de noms d’identité de l’entité du profil associé. Cette valeur suit les mêmes règles que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Si `schema.name` correspond à &quot;_xdm.context.experienceevent&quot;, cette valeur doit spécifier l’espace de noms d’identité pour l’entité spécifiée dans `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtre les données renvoyées dans la réponse. Utilisez cette option pour spécifier les valeurs des champs de schéma à inclure dans les données récupérées. Pour les champs multiples, séparez les valeurs par une virgule sans ajouter d’espace | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifie la politique de fusion qui doit régir les données renvoyées. Si l’un d’eux n’est pas spécifié dans l’appel, la valeur par défaut de votre organisation pour ce schéma sera utilisée. Si aucune politique de fusion par défaut n’a été configurée, la valeur par défaut est l’absence de fusion de profils et de combinaison d’identités. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | L’ordre de tri des événements d’expérience récupérés par date et heure, indiqué par `(+/-)timestamp`, la valeur par défaut étant `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Spécifiez l’heure de début pour filtrer les objets de série temporelle (en millisecondes). | `startTime=1539838505` |
| `endTime` | Spécifiez l’heure de fin pour filtrer les objets de série temporelle (en millisecondes). | `endTime=1539838510` |
| `limit` | Valeur numérique spécifiant le nombre maximal d’objets à renvoyer. Valeur par défaut : 1000 | `limit=100` |
| `property` | Filtre selon la valeur de la propriété. Prend en charge les évaluateurs suivants : =, !=, &lt;, &lt;=, >, >=. Peut uniquement être utilisé avec des événements d’expérience, avec un maximum de trois propriétés prises en charge. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | Indicateur de fonction permettant d’activer les attributs calculés pour la recherche. Valeur par défaut : false | `withCA=true` |
