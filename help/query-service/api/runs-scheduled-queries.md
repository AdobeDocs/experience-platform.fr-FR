---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de Query Service
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 94%

---


# Exécutions pour les requêtes planifiées

## Exemples d’appels API

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Query Service] API. The following sections walk through the various API calls you can make using the [!DNL Query Service] API. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’une liste de toutes les exécutions pour une requête planifiée spécifiée

Vous pouvez récupérer une liste de toutes les exécutions pour une requête planifiée spécifique, qu’elles soient en cours ou déjà terminées. Pour ce faire, effectuez une requête GET sur le point de terminaison `/schedules/{SCHEDULE_ID}/runs`, où `{SCHEDULE_ID}` correspond à la valeur `id` de la requête planifiée dont vous souhaitez récupérer les exécutions.

**Format d’API**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La valeur `id` de la requête planifiée que vous souhaitez récupérer. |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Les paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les exécutions pour une requête planifiée spécifiée. Tous ces paramètres sont facultatifs. En passant un appel vers ce point de terminaison sans paramètres, vous récupérerez toutes les exécutions disponibles pour une requête planifiée spécifiée.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Spécifie le champ de référence pour le tri des résultats. Les champs `created` et `updated` sont pris en charge. Par exemple, `orderby=created` triera les résultats par ordre croissant de création. L’ajout d’un `-` devant created (`orderby=-created`) triera les éléments par ordre décroissant de création. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Valeur par défaut : 20*) |
| `start` | Décale la liste de réponses à l’aide d’une numérotation à partir de zéro. Par exemple, `start=2` renvoie une liste commençant par la troisième requête répertoriée. (*Valeur par défaut : 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs `created`, `state` et `externalTrigger` sont pris en charge. Les opérateurs `>` (supérieur à), `<` (inférieur à), `==` (égal à) et `!=` (différent de) sont pris en charge. Par exemple, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` renverra toutes les exécutions créées manuellement, réussies et créées après le 20 avril 2019. |

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

Une réponse réussie renvoie un état HTTP 200 avec une liste d’exécutions pour la requête planifiée spécifiée en tant que JSON. La réponse suivante renvoie les quatre dernières exécutions pour la requête planifiée spécifiée.

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
>Vous pouvez utiliser la valeur de `_links.cancel` pour [arrêter une exécution pour une requête planifiée spécifiée](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Déclenchement immédiat d’une exécution pour une requête planifiée spécifique

Vous pouvez immédiatement déclencher une exécution pour une requête planifiée spécifiée en effectuant une requête POST sur le point de terminaison `/schedules/{SCHEDULE_ID}/runs`, où `{SCHEDULE_ID}` correspond à la valeur `id` de la requête planifiée dont vous souhaitez déclencher l’exécution.

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

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Récupération des détails d’une exécution pour une requête planifiée spécifique

Vous pouvez récupérer les détails d’une exécution pour une requête planifiée spécifique en effectuant une requête GET sur le point de terminaison `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` et en fournissant les identifiants de la requête planifiée et de l’exécution dans le chemin de requête.

**Format d’API**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La valeur `id` de la requête planifiée dont vous souhaitez récupérer les détails de l’exécution. |
| `{RUN_ID}` | La valeur `id` de l’exécution que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de l’exécution spécifiée.

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

### Arrêt immédiat d’une exécution pour une requête planifiée spécifique

Vous pouvez immédiatement arrêter une exécution pour une requête planifiée spécifique en effectuant une requête PATCH sur le point de terminaison `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` et en fournissant les identifiants de la requête planifiée et de l’exécution dans le chemin de requête.

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La valeur `id` de la requête planifiée dont vous souhaitez récupérer les détails de l’exécution. |
| `{RUN_ID}` | La valeur `id` de l’exécution que vous souhaitez récupérer. |

**Requête**

Cette requête API utilise la syntaxe du correctif JSON pour son payload. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document Principes de base des API.

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

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
