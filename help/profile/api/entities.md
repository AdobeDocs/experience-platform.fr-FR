---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API Entités (accès au profil)
type: Documentation
description: Adobe Experience Platform vous permet d’accéder aux données du profil client en temps réel à l’aide des API RESTful ou de l’interface utilisateur. Ce guide explique comment accéder aux entités, plus communément appelées « profils », à l’aide de l’API Profile.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 2f32cae89d69f6dc2930c3908c87b79e1b724f4b
workflow-type: tm+mt
source-wordcount: '2211'
ht-degree: 29%

---

# Point d&#39;entrée des entités (accès au profil)

Adobe Experience Platform vous permet d’accéder aux données [!DNL Real-Time Customer Profile] à l’aide des API RESTful ou de l’interface utilisateur. Ce guide explique comment accéder aux entités, plus communément appelées « profils », à l’aide de l’API. Pour plus d’informations sur l’accès aux profils à l’aide de l’interface utilisateur de [!DNL Experience Platform], reportez-vous au guide d’utilisation [Profile](../ui/user-guide.md).

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Résolution de l’entité

Dans le cadre de la mise à niveau de l’architecture, Adobe introduit la résolution d’entités pour les comptes et les opportunités, à l’aide d’une correspondance d’identifiants déterministe basée sur les dernières données. Le traitement de résolution d’entité s’exécute quotidiennement pendant la segmentation par lots, avant d’évaluer les audiences à entités multiples avec des attributs B2B.

Cette amélioration permet à Experience Platform d’identifier et d’unifier plusieurs enregistrements représentant la même entité, ce qui améliore la cohérence des données et permet une segmentation d’audience plus précise.

Auparavant, Comptes et opportunités s’appuyait sur une résolution basée sur un graphique d’identités qui connectait les identités, y compris toutes les ingestions historiques. Dans la nouvelle approche de résolution d’entité, les identités sont liées en fonction des données les plus récentes uniquement.

- Le compte et l’opportunité sont résolus par une fusion basée sur la priorité temporelle :
   - Compte : identités utilisant l’espace de noms `b2b_account`.
   - Opportunité : identités utilisant l’espace de noms `b2b_opportunity`.
- Toutes les autres entités sont simplement unifiées et seuls les chevauchements d’identités principales sont fusionnés avec la fusion basée sur la priorité temporelle.

>[!NOTE]
>
>La résolution d&#39;entité ne prend en charge que les `b2b_account` et les `b2b_opportunity`. Les identités d’autres espaces de noms ne sont pas utilisées dans la résolution d’entités. Si vous utilisez des espaces de noms personnalisés, vous ne pourrez pas trouver de comptes ni d’opportunités.

### Comment fonctionne la résolution d’entité ?

- **Auparavant** : si un numéro DUNS (Data Universal Numbering System) était utilisé comme identité supplémentaire et que le numéro DUNS du compte était mis à jour dans un système source tel que CRM, l’identifiant de compte est lié à la fois aux anciens et aux nouveaux numéros DUNS.
- **Après** : si le numéro DUNS a été utilisé comme identité supplémentaire et que le numéro DUNS du compte a été mis à jour dans un système source tel qu’un CRM, l’identifiant de compte n’est lié qu’au nouveau numéro DUNS, reflétant ainsi plus précisément l’état actuel du compte.

Suite à cette mise à jour, l’API [!DNL Profile Access] reflète désormais la dernière vue de profil de fusion une fois qu’un cycle de tâche de résolution d’entité est terminé. En outre, les données cohérentes fournissent des cas d’utilisation tels que la segmentation, l’activation et l’analyse avec une précision et une cohérence accrues des données.

## Récupération d’une entité {#retrieve-entity}

>[!IMPORTANT]
>
>Les entités B2B suivantes ne sont plus prises en charge pour les requêtes de recherche via l’API : **Relation compte-personne, relation opportunité-personne, campagne, membre de campagne, liste marketing et membre de liste marketing**.
>
>La prise en charge de ces entités est obsolète. Si vous disposez d’intégrations ou de workflows qui dépendent de l’accès à ces entités, mettez-les à jour pour utiliser les types d’entités pris en charge afin d’assurer la continuité des fonctionnalités.

Vous pouvez récupérer une entité de profil en adressant une requête GET au point d’entrée `/access/entities` avec les paramètres de requête requis.

>[!BEGINTABS]

>[!TAB Entité de profil]

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Les paramètres de requête fournis dans le chemin de la requête spécifient les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres séparés par des esperluettes (&amp;).

Pour accéder à une entité de profil, vous **devez** fournir les paramètres de requête suivants :

- `schema.name` : nom du schéma XDM de l’entité. Dans ce cas d’utilisation, la `schema.name=_xdm.context.profile` .
- `entityId` : ID de l’entité que vous essayez de récupérer.
- `entityIdNS` : espace de noms de l’entité que vous essayez de récupérer. Cette valeur doit être fournie si le `entityId` n’est **pas** un XID.

En outre, l’utilisation du paramètre de requête suivant est *vivement* recommandée :

- `mergePolicyId` : ID de la politique de fusion avec laquelle vous souhaitez filtrer les données. Si aucune politique de fusion n’est spécifiée, la politique de fusion par défaut de votre organisation est utilisée.

Une liste complète de paramètres valides est fournie dans la section des [paramètres de requête](#query-parameters) de l’annexe.

**Requête**

La requête suivante récupère l’adresse e-mail et le nom d’un client à l’aide d’une identité.

+++ Exemple de requête pour récupérer une entité à l’aide d’une identité

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec l’entité demandée.

+++ Exemple de réponse contenant l’entité demandée

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
                    "id": "johnsmith@example.com",
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

+++

>[!NOTE]
>
>Si un graphique associé lie plus de 50 identités, ce service renvoie un état HTTP 422 et le message « Trop d’identités connexes ». Si cette erreur s’affiche, pensez à ajouter d’autres paramètres de requête pour affiner votre recherche.

>[!TAB Compte B2B]

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Les paramètres de requête fournis dans le chemin de la requête spécifient les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres séparés par des esperluettes (&amp;).

Pour accéder aux données du compte B2B, vous **devez** fournir les paramètres de requête suivants :

- `schema.name` : nom du schéma XDM de l’entité. Dans ce cas d’utilisation, cette valeur est `schema.name=_xdm.context.account`.
- `entityId` : ID de l’entité que vous essayez de récupérer.
- `entityIdNS` : espace de noms de l’entité que vous essayez de récupérer. Cette valeur doit être fournie si le `entityId` n’est **pas** un XID.

En outre, l’utilisation du paramètre de requête suivant est *vivement* recommandée :

- `mergePolicyId` : ID de la politique de fusion avec laquelle vous souhaitez filtrer les données. Si aucune politique de fusion n’est spécifiée, la politique de fusion par défaut de votre organisation est utilisée.

Une liste complète de paramètres valides est fournie dans la section des [paramètres de requête](#query-parameters) de l’annexe.

**Requête**

+++ Exemple de requête pour récupérer un compte B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec l’entité demandée.

+++ Exemple de réponse contenant l’entité demandée

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB  Opportunité B2B ]

**Format d’API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Les paramètres de requête fournis dans le chemin de la requête spécifient les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres séparés par des esperluettes (&amp;).

Pour accéder à une entité d’opportunité B2B, vous **devez** fournir les paramètres de requête suivants :

- `schema.name` : nom du schéma XDM de l’entité. Dans ce cas d’utilisation, la `schema.name=_xdm.context.opportunity` .
- `entityId` : ID de l’entité que vous essayez de récupérer.
- `entityIdNS` : espace de noms de l’entité que vous essayez de récupérer. Cette valeur doit être fournie si le `entityId` n’est **pas** un XID.

En outre, l’utilisation du paramètre de requête suivant est *vivement* recommandée :

- `mergePolicyId` : ID de la politique de fusion avec laquelle vous souhaitez filtrer les données. Si aucune politique de fusion n’est spécifiée, la politique de fusion par défaut de votre organisation est utilisée.

Une liste complète de paramètres valides est fournie dans la section des [paramètres de requête](#query-parameters) de l’annexe.

**Requête**

+++ Exemple de requête pour récupérer une entité opportunité B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec l’entité demandée.

+++ Exemple de réponse contenant l’entité demandée

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Récupération de plusieurs entités {#retrieve-entities}

Vous pouvez récupérer plusieurs entités de profil en adressant une requête POST au point d’entrée `/access/entities` et en fournissant les identités dans la payload.

>[!BEGINTABS]

>[!TAB Entités de profil]

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les noms et adresses e-mail de plusieurs clients à l’aide d’une liste d’identités.

+++Exemple de requête pour récupérer plusieurs entités

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp"
      }'
```

| Propriété | Type | Description |
| -------- |----- | ----------- |
| `schema.name` | Chaîne | **(Obligatoire)** Le nom du schéma XDM auquel appartient l’entité. |
| `fields` | Tableau | Les champs XDM à renvoyer, sous forme de tableau de chaînes. Tous les champs sont renvoyés par défaut. |
| `identities` | Tableau | **(Obligatoire)** Un tableau contenant une liste d’identités pour les entités auxquelles vous souhaitez accéder. |
| `identities.entityId` | Chaîne | L’identifiant d’une entité à laquelle vous souhaitez accéder. |
| `identities.entityIdNS.code` | Chaîne | L’espace de noms d’un identifiant d’entité auquel vous souhaitez accéder. |
| `timeFilter.startTime` | Nombre entier | Indique l’heure de début du filtrage des entités de profil (en millisecondes). Par défaut, cette valeur est définie comme le début du temps disponible. |
| `timeFilter.endTime` | Nombre entier | Indique l’heure de fin du filtrage des entités de profil (en millisecondes). Par défaut, cette valeur est définie comme la fin du temps disponible. |
| `limit` | Nombre entier | Nombre maximal d’enregistrements à renvoyer. Par défaut, cette valeur est définie sur 1000. |
| `orderby` | Chaîne | L’ordre de tri des événements d’expérience récupérés par date et heure, indiqué par `(+/-)timestamp`, la valeur par défaut étant `+timestamp`. |

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec les champs demandés des entités spécifiées dans le corps de la requête.

+++ Exemple de réponse contenant les entités demandées

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

+++

>[!TAB Compte B2B]

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les comptes B2B demandés.

+++Exemple de requête pour récupérer plusieurs entités

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Propriété | Type | Description |
| -------- |----- | ----------- |
| `schema.name` | Chaîne | **(Obligatoire)** Le nom du schéma XDM auquel appartient l’entité. |
| `identities` | Tableau | **(Obligatoire)** Un tableau contenant une liste d’identités pour les entités auxquelles vous souhaitez accéder. |
| `identities.entityId` | Chaîne | L’identifiant d’une entité à laquelle vous souhaitez accéder. |
| `identities.entityIdNS.code` | Chaîne | L’espace de noms d’un identifiant d’entité auquel vous souhaitez accéder. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les entités demandées.

+++ Exemple de réponse contenant les entités demandées

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB  Opportunité B2B ]

**Format d’API**

```http
POST /access/entities
```

**Requête**

La requête suivante récupère les opportunités B2B demandées.

+++ Exemple de requête pour récupérer plusieurs entités

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Propriété | Type | Description |
| -------- |----- | ----------- |
| `schema.name` | Chaîne | **(Obligatoire)** Le nom du schéma XDM auquel appartient l’entité. |
| `identities` | Tableau | **(Obligatoire)** Un tableau contenant une liste d’identités pour les entités auxquelles vous souhaitez accéder. |
| `identities.entityId` | Chaîne | L’identifiant d’une entité à laquelle vous souhaitez accéder. |
| `identities.entityIdNS.code` | Chaîne | L’espace de noms d’un identifiant d’entité auquel vous souhaitez accéder. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les entités demandées.

+++ Exemple de réponse contenant les entités demandées

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Accès à une page de résultats ultérieure

Les résultats sont paginés lors de la récupération des événements de série temporelle. Si des pages de résultats ultérieures sont disponibles, la propriété `_page.next` contiendra un identifiant. En outre, la propriété `_links.next.href` fournit un URI de requête pour récupérer la page suivante. Pour récupérer les résultats, envoyez une autre requête GET au point d’entrée `/access/entities` et remplacez `/entities` par la valeur de l’URI fourni.

>[!NOTE]
>
>Assurez-vous de ne pas répéter accidentellement `/entities/` dans le chemin d’accès de la requête. Il ne doit apparaître qu’une seule fois, par exemple : `/access/entities?start=...`

**Format d’API**

```http
GET /access/{NEXT_URI}
```

| Paramètre | Description |
|---|---|
| `{NEXT_URI}` | La valeur URI provenant de `_links.next.href`. |

**Requête**

La requête suivante récupère la page de résultats suivante en utilisant l’URI `_links.next.href` comme chemin de requête.

+++ Exemple de requête d’accès à la page de résultats suivante

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie la page de résultats suivante. Cette réponse ne comporte pas de pages de résultats ultérieures, comme indiqué par les valeurs de chaîne vides de `_page.next` et `_links.next.href`.

+++ Exemple de réponse contenant la page suivante d’entités

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

+++

## Suppression d’une entité {#delete-entity}

>[!IMPORTANT]
>
>Le point d’entrée de suppression d’entité sera abandonné d’ici la fin octobre 2025. Si vous souhaitez effectuer des opérations de suppression d’enregistrements, vous pouvez utiliser le workflow [&#x200B; API de suppression des enregistrements du cycle de vie des données &#x200B;](/help/hygiene/api/workorder.md) ou le workflow de l’interface utilisateur de suppression des enregistrements du cycle de vie des données [&#128279;](/help/hygiene/ui/record-delete.md) à la place.
>
>En outre, les requêtes de suppression pour les entités B2B suivantes ont déjà été abandonnées :
>
>- Compte
>- Relation Compte-Personne
>- Opportunité
>- Relation Opportunité-Personne
>- Campagne
>- Membre de la campagne
>- Liste marketing
>- Membres de la liste marketing

Vous pouvez supprimer une entité du magasin de profils en adressant une requête DELETE au point d’entrée `/access/entities` avec les paramètres de requête requis.

**Format d’API**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

Les paramètres de requête fournis dans le chemin de la requête spécifient les données auxquelles accéder. Vous pouvez inclure plusieurs paramètres séparés par des esperluettes (&amp;).

Pour supprimer une entité, vous **devez** fournir les paramètres de requête suivants :

- `schema.name` : nom du schéma XDM de l’entité. Dans ce cas d’utilisation, vous pouvez **uniquement** utiliser `schema.name=_xdm.context.profile`.
- `entityId` : ID de l’entité que vous essayez de récupérer.
- `entityIdNS` : espace de noms de l’entité que vous essayez de récupérer. Cette valeur doit être fournie si le `entityId` n’est **pas** un XID.
- `mergePolicyId` : ID de la politique de fusion de l’entité. La politique de fusion contient des informations sur le groupement d’identités et la fusion d’objets XDM clé-valeur. Si cette valeur n’est pas fournie, la politique de fusion par défaut est utilisée.

**Requête**

La requête suivante supprime l’entité spécifiée.

+++ Exemple de requête pour supprimer une entité

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 202 avec un corps de réponse vide.

## Étapes suivantes

En suivant ce guide, vous avez accédé avec succès aux champs de données [!DNL Real-Time Customer Profile], aux profils et aux données de série temporelle. Pour découvrir comment accéder à d’autres ressources de données stockées dans [!DNL Experience Platform], consultez la [présentation de Data Access](../../data-access/home.md).

## Annexe {#appendix}

La section suivante fournit des informations supplémentaires sur l’accès aux données [!DNL Profile] à l’aide de l’API .

### Paramètres de requête {#query-parameters}

Les paramètres suivants sont utilisés dans le chemin des requêtes GET vers le point d’entrée `/access/entities`. Ils permettent d’identifier l’entité de profil à laquelle vous souhaitez accéder et de filtrer les données renvoyées dans la réponse. Les paramètres requis sont signalés par un libellé, tandis que les autres sont facultatifs.

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `schema.name` | **(Obligatoire)** Nom du schéma XDM de l’entité. | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | Si `schema.name` est `_xdm.context.experienceevent`, cette valeur **doit** spécifie le schéma de l’entité de profil à laquelle les événements de série temporelle sont associés. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Obligatoire)** Identifiant de l’entité. Si la valeur de ce paramètre n’est pas un XID, un paramètre d’espace de noms d’identité (`entityIdNS`) doit également être fourni. | `entityId=janedoe@example.com` |
| `entityIdNS` | Si `entityId` n’est pas fourni sous forme de XID, ce champ **doit** spécifie l’espace de noms d’identité. | `entityIdNS=email` |
| `relatedEntityId` | Si `schema.name` est `_xdm.context.experienceevent`, cette valeur **doit** spécifie l’identifiant de l’entité de profil associée. Cette valeur suit les mêmes règles que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Si `schema.name` correspond à &quot;_xdm.context.experienceevent&quot;, cette valeur doit spécifier l’espace de noms d’identité pour l’entité spécifiée dans `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtre les données renvoyées dans la réponse. Utilisez cette option pour spécifier les valeurs des champs de schéma à inclure dans les données récupérées. Pour plusieurs champs, séparez les valeurs par une virgule sans espaces entre. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | *Recommandé* identifie la politique de fusion selon laquelle gérer les données renvoyées. Si l’un d’eux n’est pas spécifié dans l’appel, la valeur par défaut de votre organisation pour ce schéma sera utilisée. Si aucune politique de fusion par défaut n’a été définie pour le schéma que vous demandez, l’API renvoie un code de statut d’erreur HTTP 422. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Ordre de tri des entités récupérées par horodatage. Il est écrit comme `(+/-)timestamp`, la valeur par défaut étant `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Indique l’heure de début pour le filtrage des entités (en millisecondes). | `startTime=1539838505` |
| `endTime` | Indique l’heure de fin du filtrage des entités (en millisecondes). | `endTime=1539838510` |
| `limit` | Spécifie le nombre maximal d&#39;entités à renvoyer. Par défaut, cette valeur est définie sur 1000. | `limit=100` |
| `property` | Filtre en fonction de la valeur de la propriété. Ce paramètre de requête prend en charge les évaluateurs suivants : =, !=, &lt;, &lt;=, >, >=. Elle ne peut être utilisée qu’avec des événements d’expérience, trois propriétés au maximum étant prises en charge. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
