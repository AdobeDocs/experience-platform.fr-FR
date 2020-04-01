---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur du service '
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# S’exécute pour les  planifiées

## Exemples d’appels d’API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels à l’API du service . Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API de service . Chaque appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupérer un  de toutes les exécutions pour un planifié spécifique 

Vous pouvez récupérer un  de toutes les exécutions pour un  de planifié spécifique, qu’il soit en cours d’exécution ou déjà terminé. Pour ce faire, vous devez envoyer une requête GET au `/schedules/{SCHEDULE_ID}/runs` point de terminaison, où `{SCHEDULE_ID}` correspond à la `id` valeur du planifié dont vous souhaitez récupérer les exécutions.

**Format API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planifié que vous souhaitez récupérer. |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres**

Vous trouverez ci-dessous un de paramètres de disponibles pour les exécutions de liste d’une  planifiée spécifiée. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètre récupère toutes les exécutions disponibles pour le  planifié spécifié.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ de commande des résultats. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. L’ajout d’un élément `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale le  de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie un  commençant à partir du troisième répertorié. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Le **doit** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs jeux de  de. Les champs pris en charge sont `created`, `state`et `externalTrigger`. Les  des opérateurs pris en charge sont `>` (supérieur à), `<` (inférieur à) et `==` (égal à) et `!=` (différent de). Par exemple, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` renverra toutes les exécutions qui ont été créées manuellement, réussies et créées après le 20 avril 2019. |

**Requête**

La requête suivante récupère les quatre dernières exécutions pour le  planifié spécifié.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un d’exécutions pour le planifié spécifié  en tant que JSON. La réponse suivante renvoie les quatre dernières exécutions pour le  planifié spécifié.

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

>[!NOTE] Vous pouvez utiliser la valeur de `_links.cancel` pour [arrêter une exécution pour un](#immediately-stop-a-run-for-a-specific-scheduled-query)planifié spécifié.

### Déclenchez immédiatement une exécution pour un planifié spécifique 

Vous pouvez immédiatement déclencher une exécution pour un planifié spécifié en faisant une requête POST au `/schedules/{SCHEDULE_ID}/runs` point de fin, où `{SCHEDULE_ID}` correspond à la `id` valeur du planifié  dont vous souhaitez déclencher l’exécution.

**Format API**

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

### Récupération des détails d’une exécution pour un planifié spécifique 

Vous pouvez récupérer les détails d’une exécution pour un  planifié spécifique en faisant une requête GET au `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` point de fin et en fournissant l’ID du  planifié et l’exécution dans le chemin de requête.

**Format API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du  planifié dont vous souhaitez récupérer les détails. |
| `{RUN_ID}` | Valeur `id` de l’exécution que vous souhaitez récupérer. |

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

### Arrêter immédiatement une exécution pour un planifié spécifique 

Vous pouvez immédiatement arrêter une exécution pour un  planifié spécifique en faisant une requête PATCH au point de `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` fin et en fournissant l’ID du planifié et l’exécution dans le chemin de requête.

**Format API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du  planifié dont vous souhaitez récupérer les détails. |
| `{RUN_ID}` | Valeur `id` de l’exécution que vous souhaitez récupérer. |

**Requête**

Cette requête d’API utilise la syntaxe du correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le des fondamentaux de l’API.

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
