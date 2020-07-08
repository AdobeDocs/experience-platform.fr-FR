---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur Requête Service
topic: scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 6%

---


# requêtes planifiées

## Exemples d’appels d’API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Requête Service. Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API Requête Service. Chaque appel comprend le format général de l’API, un exemple de requête indiquant les en-têtes requis et un exemple de réponse.

### Récupération d’une liste de requêtes planifiées

You can retrieve a list of all scheduled queries for your IMS Organization by making a GET request to the `/schedules` endpoint.

**Format d’API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Optional*) Parameters added to the request path which configure the results returned in the response. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Voici une liste des paramètres de requête disponibles pour répertorier les requêtes planifiées. Tous ces paramètres sont facultatifs. L&#39;appel à ce point de terminaison sans paramètre récupère toutes les requêtes planifiées disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ selon lequel les résultats doivent être commandés. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. Ajouter un `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale la liste de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie une liste commençant à partir de la troisième requête répertoriée. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs pris en charge sont `created`, `templateId`et `userId`. La liste des opérateurs pris en charge est `>` (supérieure à), `<` (inférieure à) et `==` (égale à). Par exemple, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie toutes les requêtes planifiées où l’ID utilisateur est spécifié. |

**Requête**

La requête suivante récupère la dernière requête planifiée créée pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste de requêtes planifiées pour l’organisation IMS spécifiée. La réponse suivante renvoie la dernière requête planifiée créée pour votre organisation IMS.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Créer une nouvelle requête planifiée

You can create a new scheduled query by making a POST request to the `/schedules` endpoint.

**Format d’API**

```http
POST /schedules
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Propriété | Description |
| -------- | ----------- |
| `query.dbName` | Nom de la base de données pour laquelle vous créez une requête planifiée. |
| `query.sql` | requête SQL que vous souhaitez créer. |
| `query.name` | Nom de la requête planifiée. |
| `schedule.schedule` | Le calendrier cron de la requête. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [d&#39;expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. Dans cet exemple, &quot;30 * * * *&quot; signifie que la requête s’exécute toutes les heures à la note de 30 minutes. |
| `schedule.startDate` | Date de début de votre requête planifiée, écrite en tant qu’horodatage UTC. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec les détails de votre nouvelle requête planifiée. Une fois que la requête planifiée est activée, elle `state` passe de `REGISTERING` à `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer la requête](#delete-a-specified-scheduled-query)planifiée que vous avez créée.

### Demander les détails d&#39;une requête planifiée spécifiée

Vous pouvez récupérer des informations pour une requête planifiée spécifique en envoyant une requête GET au point de `/schedules` terminaison et en indiquant son identifiant dans le chemin de requête.

**Format d’API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the scheduled query you want to retrieve. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de la requête planifiée spécifiée.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer la requête](#delete-a-specified-scheduled-query)planifiée que vous avez créée.

### Mettre à jour les détails d’une requête planifiée spécifiée

Vous pouvez mettre à jour les détails d’une requête planifiée spécifiée en envoyant une requête PATCH au point de `/schedules` terminaison et en indiquant son identifiant dans le chemin de requête.

La demande PATCH prend en charge deux chemins différents : `/state` et `/schedule/schedule`.

### Mettre à jour l&#39;état de la requête planifiée

Vous pouvez utiliser `/state` pour mettre à jour l&#39;état de la requête planifiée sélectionnée - ACTIVÉE ou DÉSACTIVÉE. Pour mettre à jour l’état, vous devez définir la valeur comme `enable` ou `disable`.

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the scheduled query you want to retrieve. |


**Requête**

Cette requête d’API utilise la syntaxe de correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document de base de l’API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `path` | Chemin d’accès de la valeur à appliquer. Dans ce cas, puisque vous mettez à jour l’état de la requête planifiée, vous devez définir la valeur de `path` sur `/state`. |
| `value` | Valeur mise à jour de la `/state`. Cette valeur peut être définie sur `enable` ou `disable` pour activer ou désactiver la requête planifiée. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Mettre à jour la planification de la requête planifiée

Vous pouvez utiliser `/schedule/schedule` pour mettre à jour la planification cron de la requête planifiée. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [d&#39;expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the scheduled query you want to retrieve. |

**Requête**

Cette requête d’API utilise la syntaxe de correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document de base de l’API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `path` | Chemin d’accès de la valeur à appliquer. Dans ce cas, puisque vous mettez à jour la planification de la requête planifiée, vous devez définir la valeur de `path` sur `/schedule/schedule`. |
| `value` | Valeur mise à jour de la `/schedule`. Cette valeur doit prendre la forme d’un calendrier cron. Dans cet exemple, la requête planifiée s’exécute toutes les heures à la barre des 45 minutes. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Supprimer une requête planifiée spécifiée

Vous pouvez supprimer une requête planifiée spécifiée en adressant une requête de DELETE au point de `/schedules` terminaison et en indiquant l’identifiant de la requête planifiée que vous souhaitez supprimer dans le chemin de la requête.

>[!NOTE]
>
>La planification **doit** être désactivée avant d&#39;être supprimée.

**Format d’API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the scheduled query you want to retrieve. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
