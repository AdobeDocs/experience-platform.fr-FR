---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur du service '
topic: scheduled queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


#  de planifié

## Exemples d’appels d’API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels à l’API du service . Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API de service . Chaque appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Récupération d’un  de planifié 

Vous pouvez récupérer un de tous les  planifiés pour votre organisation IMS en envoyant une requête GET au point de `/schedules` terminaison.

**Format API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres**

Vous trouverez ci-dessous un  de paramètres de disponibles pour répertorier les  de l’ programmée. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètre récupérera tous les  planifiés disponibles pour votre entreprise.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Indique le champ de commande des résultats. Les champs pris en charge sont `created` et `updated`. Par exemple, `orderby=created` triera les résultats par ordre croissant. L’ajout d’un élément `-` avant création (`orderby=-created`) triera les éléments par création dans l’ordre décroissant. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Default value: 20*) |
| `start` | Décale le  de réponse à l’aide d’une numérotation à base zéro. Par exemple, `start=2` renvoie un  commençant à partir du troisième répertorié. (*Default value: 0*) |
| `property` | Filtrez les résultats en fonction des champs. Le **doit** être une séquence d’échappement HTML. Les virgules sont utilisées pour combiner plusieurs jeux de  de. Les champs pris en charge sont `created`, `templateId`et `userId`. Les  des opérateurs pris en charge sont `>` (supérieur à), `<` (inférieur à) et `==` (égal à). Par exemple, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie tous les planifiés pour lesquels l’ID utilisateur est tel que spécifié. |

**Requête**

La requête suivante récupère le dernier  planifié créé pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un de planifiés  pour l’organisation IMS spécifiée. La réponse suivante renvoie le dernier  planifié créé pour votre organisation IMS.

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

### Création d’un planifié 

Vous pouvez créer un nouvel  planifié en envoyant une requête POST au point de `/schedules` fin.

**Format API**

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
| `query.dbName` | Nom de la base de données pour laquelle vous créez un planifié. |
| `query.sql` | Le SQL  que vous souhaitez créer. |
| `query.name` | Nom du  planifié. |
| `schedule.schedule` | Le calendrier cron pour le . Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [de ](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron . Dans cet exemple, &quot;30 * * * *&quot; signifie que le s’exécute toutes les heures à la note de 30 minutes. |
| `schedule.startDate` | Date  de votre planifié , écrite en tant qu’horodatage UTC. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec les détails de vos nouveaux  planifiés. Une fois que le  planifié est activé, il `state` passe de `REGISTERING` à `ENABLED`.

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

>[!NOTE] Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer les](#delete-a-specified-scheduled-query)planifiées que vous avez créées.

### Demander les détails d’un planifié spécifié 

Vous pouvez récupérer les informations d’un planifié spécifique en faisant une requête GET au point de `/schedules` fin et en indiquant son ID dans le chemin d’accès à la requête.

**Format API**

```http
GET /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planifié que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails du  planifié spécifié.

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

>[!NOTE] Vous pouvez utiliser la valeur de `_links.delete` pour [supprimer les](#delete-a-specified-scheduled-query)planifiées que vous avez créées.

### Mettre à jour les détails d’un planifié spécifié 

Vous pouvez mettre à jour les détails d’un planifié spécifié en effectuant une requête PATCH sur le `/schedules` point de fin et en indiquant son ID dans le chemin d’accès de la requête.

La requête PATCH prend en charge deux chemins différents : `/state` et `/schedule/schedule`.

### Mettre à jour l&#39;état  du planifié

Vous pouvez utiliser `/state` pour mettre à jour l’état du planifié sélectionné - Activé ou Désactivé. Pour mettre à jour l’état, vous devez définir la valeur sur `enable` ou `disable`.

**Format API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planifié que vous souhaitez récupérer. |


**Requête**

Cette requête d’API utilise la syntaxe du correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le des fondamentaux de l’API.

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
| `path` | Chemin d’accès de la valeur que vous souhaitez appliquer au correctif. Dans ce cas, puisque vous mettez à jour l’état  du planifié, vous devez définir la valeur de `path` sur `/state`. |
| `value` | Valeur mise à jour de la `/state`. Cette valeur peut être définie sur `enable` ou `disable` pour activer ou désactiver le  planifié. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Mettre à jour le calendrier des  planifiées

Vous pouvez utiliser `/schedule/schedule` pour mettre à jour la planification cron du  planifié. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [de ](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron .

**Format API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planifié que vous souhaitez récupérer. |

**Requête**

Cette requête d’API utilise la syntaxe du correctif JSON pour sa charge utile. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le des fondamentaux de l’API.

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
| `path` | Chemin d’accès de la valeur que vous souhaitez appliquer au correctif. Dans ce cas, étant donné que vous mettez à jour le calendrier  planifié, vous devez définir la valeur de `path` sur `/schedule/schedule`. |
| `value` | Valeur mise à jour de la `/schedule`. Cette valeur doit prendre la forme d’un calendrier cron. Dans cet exemple, le  planifié s’exécutera toutes les heures à la note de 45 minutes. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) avec le message suivant.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Supprimer un planifié spécifié 

Vous pouvez supprimer un  planifié spécifié en faisant une requête DELETE au point de `/schedules` fin et en indiquant l’ID du planifié à supprimer dans le chemin d’accès à la requête.

>[!NOTE] La planification **doit** être désactivée avant d’être supprimée.

**Format API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planifié que vous souhaitez récupérer. |

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
