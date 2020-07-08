---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur Requête Service
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 6%

---


# S’exécute pour les requêtes planifiées.

## Exemples d’appels d’API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Requête Service. Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API Requête Service. Chaque appel comprend le format général de l’API, un exemple de requête indiquant les en-têtes requis et un exemple de réponse.

### Récupérer une liste de toutes les exécutions pour une requête planifiée spécifiée

Vous pouvez récupérer une liste de toutes les exécutions pour une requête planifiée spécifique, qu’elles soient en cours d’exécution ou déjà terminées. Pour ce faire, vous devez envoyer une requête GET au point de `/schedules/{SCHEDULE_ID}/runs` terminaison, où `{SCHEDULE_ID}` correspond à la valeur `id` de la requête planifiée dont vous souhaitez récupérer les exécutions.

**Format d’API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the scheduled query you want to retrieve. |
| `{QUERY_PARAMETERS}` | (*Optional*) Parameters added to the request path which configure the results returned in the response. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Voici une liste des paramètres de requête disponibles pour les exécutions de liste pour une requête planifiée spécifiée. Tous ces paramètres sont facultatifs. L’exécution d’un appel à ce point de terminaison sans paramètres récupérera toutes les exécutions disponibles pour la requête planifiée spécifiée.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ selon lequel les résultats doivent être commandés. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. Ajouter un `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale la liste de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie une liste commençant à partir de la troisième requête répertoriée. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs pris en charge sont `created`, `state`et `externalTrigger`. La liste des opérateurs pris en charge est `>` (supérieure à), `<` (inférieure à) et `==` (égale à), et `!=` (différente de). Par exemple, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` renvoie toutes les exécutions qui ont été créées manuellement, qui ont réussi et qui ont été créées après le 20 avril 2019. |

**Requête**

La requête suivante récupère les quatre dernières exécutions pour la requête planifiée spécifiée.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste d’exécutions pour la requête planifiée spécifiée en tant que JSON. La réponse suivante renvoie les quatre dernières exécutions pour la requête planifiée spécifiée.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>Vous pouvez utiliser la valeur de `_links.cancel` pour [arrêter une exécution pour une requête](#immediately-stop-a-run-for-a-specific-scheduled-query)planifiée spécifiée.

### Déclencher immédiatement une exécution pour une requête planifiée spécifique

Vous pouvez immédiatement déclencher une exécution pour une requête planifiée spécifiée en envoyant une requête POST au point de `/schedules/{SCHEDULE_ID}/runs` terminaison, où `{SCHEDULE_ID}` est la valeur `id` de la requête planifiée dont vous souhaitez déclencher l&#39;exécution.

**Format d’API**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Récupération des détails d’une exécution pour une requête planifiée spécifique

Vous pouvez récupérer des détails sur une exécution pour une requête planifiée spécifique en faisant une requête GET au point de `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` terminaison et en fournissant à la fois l’ID de la requête planifiée et l’exécution dans le chemin de la requête.

**Format d’API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` de la requête planifiée dont vous souhaitez récupérer les détails. |
| `{RUN_ID}` | Valeur `id` de l&#39;exécution que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de l’exécution spécifiée.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Arrêter immédiatement une exécution pour une requête planifiée spécifique

Vous pouvez immédiatement arrêter une exécution pour une requête planifiée spécifique en exécutant une requête PATCH sur le point de `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` terminaison et en fournissant l’ID de la requête planifiée et l’exécution dans le chemin de la requête.

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` de la requête planifiée dont vous souhaitez récupérer les détails. |
| `{RUN_ID}` | Valeur `id` de l&#39;exécution que vous souhaitez récupérer. |

**Requête**

Cette requête d’API utilise la syntaxe de correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document de base de l’API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
