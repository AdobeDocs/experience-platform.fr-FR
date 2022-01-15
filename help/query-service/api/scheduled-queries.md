---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requêtes planifiées;requête planifiée;
solution: Experience Platform
title: Point de terminaison de l’API Requêtes planifiées
topic-legacy: scheduled queries
description: Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer pour les requêtes planifiées avec l’API Query Service.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: f1b982e5f788282a8cf2a9c4523370c520b82d0e
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 77%

---

# Point de terminaison des requêtes planifiées

## Exemples d’appels API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels au [!DNL Query Service] API. Les sections suivantes décrivent les différents appels API que vous pouvez effectuer à l’aide de la variable [!DNL Query Service] API. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’une liste de requêtes planifiées

Vous pouvez obtenir une liste de toutes les requêtes planifiées de votre organisation IMS en effectuant une requête GET vers le point de terminaison `/schedules`.

**Format d’API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Les paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les requêtes planifiées. Tous ces paramètres sont facultatifs. En effectuant un appel vers ce point de terminaison sans paramètres, vous récupérerez toutes les requêtes planifiées disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Spécifie le champ de référence pour le tri des résultats. Les champs `created` et `updated` sont pris en charge. Par exemple, `orderby=created` triera les résultats par ordre croissant de création. L’ajout d’un `-` devant created (`orderby=-created`) triera les éléments par ordre décroissant de création. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Valeur par défaut : 20*) |
| `start` | Décale la liste de réponses à l’aide d’une numérotation à partir de zéro. Par exemple, `start=2` renvoie une liste commençant par la troisième requête répertoriée. (*Valeur par défaut : 0*) |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs `created`, `templateId` et `userId` sont pris en charge. Les opérateurs `>` (supérieur à), `<` (inférieur à) et `==` (égal à) sont pris en charge. Par exemple, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie toutes les requêtes planifiées pour lesquelles l’identifiant utilisateur est tel qu’indiqué. |

**Requête**

La requête suivante renvoie la dernière requête planifiée créée pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de requêtes planifiées pour l’organisation IMS spécifiée. La réponse suivante renvoie la dernière requête planifiée créée pour votre organisation IMS.

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

### Création d’une requête planifiée

Vous pouvez créer une requête planifiée en effectuant une requête POST vers le point de terminaison `/schedules`. Lorsque vous créez une requête planifiée dans l’API, vous pouvez également la voir dans l’éditeur de requêtes. Pour plus d’informations sur les requêtes planifiées dans l’interface utilisateur, veuillez lire le [Documentation de Query Editor](../ui/user-guide.md#scheduled-queries).

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
| `query.sql` | La requête SQL que vous souhaitez créer. |
| `query.name` | Le nom de la requête planifiée. |
| `schedule.schedule` | Le planning cron de la requête. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 30 * * * * » signifie que la requête s’exécute toutes les heures à la 30e minute.<br><br>Vous pouvez également utiliser les expressions abrégées suivantes :<ul><li>`@once`: La requête ne s’exécute qu’une seule fois.</li><li>`@hourly`: La requête s’exécute toutes les heures au début de l’heure. Cela équivaut à l’expression cron. `0 * * * *`.</li><li>`@daily`: La requête s’exécute une fois par jour à minuit. Cela équivaut à l’expression cron. `0 0 * * *`.</li><li>`@weekly`: La requête s’exécute une fois par semaine, le dimanche, à minuit. Cela équivaut à l’expression cron. `0 0 * * 0`.</li><li>`@monthly`: La requête s&#39;exécute une fois par mois, le premier jour du mois, à minuit. Cela équivaut à l’expression cron. `0 0 1 * *`.</li><li>`@yearly`: La requête s’exécute une fois par an, le 1er janvier, à minuit. Cela équivaut à l’expression cron. `1 0 0 1 1 *`. |
| `schedule.startDate` | La date de début de votre requête planifiée, écrite en tant qu’horodatage en UTC. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec les détails de la requête planifiée que vous venez de créer. Une fois que la requête planifiée est activée, `state` passe de `REGISTERING` à `ENABLED`.

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
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer la requête planifiée créée](#delete-a-specified-scheduled-query).

### Demande des détails d’une requête planifiée spécifiée

Vous pouvez récupérer des informations sur une requête planifiée spécifique en effectuant une requête GET vers le point de terminaison `/schedules` et en fournissant son identifiant dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | La valeur `id` de la requête planifiée que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la requête planifiée spécifiée.

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
>Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer la requête planifiée créée](#delete-a-specified-scheduled-query).

### Mise à jour des détails d’une requête planifiée spécifiée

Vous pouvez mettre à jour les détails d’une requête planifiée spécifiée en effectuant une requête PATCH vers le point de terminaison `/schedules` et en fournissant son identifiant dans le chemin d’accès de la requête.

La requête PATCH prend en charge deux chemins d’accès différents : `/state` et `/schedule/schedule`.

### Mise à jour de l’état de la requête planifiée

Vous pouvez utiliser `/state` pour mettre à jour l’état de la requête planifiée sélectionnée - ACTIF ou INACTIF. Pour mettre à jour l’état, vous devez définir la valeur sur `enable` ou sur `disable`.

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur de la requête planifiée que vous souhaitez PATCH. |


**Requête**

Cette requête API utilise la syntaxe du correctif JSON pour son payload. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document principes de base des API.

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
| `path` | Chemin d’accès de la valeur que vous souhaitez mettre à jour. Dans ce cas, puisque vous mettez à jour l’état de la requête planifiée, vous devez définir la valeur de `path` sur `/state`. |
| `value` | Valeur mise à jour de `/state`. Cette valeur peut être définie sur `enable` ou sur `disable` pour activer ou désactiver la requête planifiée. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Mise à jour du planning de la requête planifiée

Vous pouvez utiliser `/schedule/schedule` pour mettre à jour le planning cron de la requête planifiée. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur de la requête planifiée que vous souhaitez PATCH. |

**Requête**

Cette requête API utilise la syntaxe du correctif JSON pour son payload. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document principes de base des API.

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
| `path` | Chemin d’accès de la valeur que vous souhaitez mettre à jour. Dans ce cas, puisque vous mettez à jour le planning de la requête planifiée, vous devez définir la valeur de `path` sur `/schedule/schedule`. |
| `value` | Valeur mise à jour de `/schedule`. Cette valeur doit se présenter sous la forme d’un planning cron. Dans cet exemple, la requête planifiée s’exécutera toutes les heures à la 45e minute. |

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Suppression d’une requête planifiée spécifiée

Vous pouvez supprimer une requête planifiée spécifiée en effectuant une requête DELETE vers le point de terminaison `/schedules` et en fournissant l’identifiant de la requête planifiée que vous souhaitez supprimer du chemin d’accès de la requête.

>[!NOTE]
>
>Le planning **doit** être désactivé avant d’être supprimé.

**Format d’API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur de la requête planifiée que vous souhaitez DELETE. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec le message suivant.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
