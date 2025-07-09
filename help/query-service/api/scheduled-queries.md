---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;requêtes planifiées;requête planifiée;
solution: Experience Platform
title: Point d’entrée des plannings
description: Les sections suivantes décrivent les différents appels API que vous pouvez effectuer pour les requêtes planifiées avec l’API Query Service.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 10c0c5c639226879b1ca25391fc4a1006cf40003
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 46%

---

# Point d’entrée des plannings

Découvrez comment créer, gérer et surveiller des requêtes planifiées par programmation à l’aide de l’API de plannings Query Service avec des informations détaillées et des exemples.

## Exigences et conditions préalables

Vous pouvez créer des requêtes planifiées à l’aide d’un compte technique (authentifié via les informations d’identification de serveur à serveur OAuth) ou d’un compte utilisateur personnel (jeton d’utilisateur). Cependant, Adobe recommande vivement d’utiliser un compte technique pour assurer l’exécution sécurisée et ininterrompue des requêtes planifiées, en particulier pour les charges de travail de production ou à long terme.

Les requêtes créées avec un compte d’utilisateur personnel échouent si l’accès de cet utilisateur est révoqué ou si son compte est désactivé. Les comptes techniques offrent une plus grande stabilité car ils ne sont pas liés au statut d’emploi ou aux droits d’accès d’un utilisateur individuel.

>[!IMPORTANT]
>
>Points importants lors de la gestion des requêtes planifiées :<ul><li>Les requêtes planifiées échouent si le compte (technique ou utilisateur) utilisé pour les créer perd l’accès ou les autorisations.</li><li>Les requêtes planifiées doivent être désactivées avant la suppression via l’API ou l’interface utilisateur.</li><li>La planification indéfinie sans date de fin n’est pas prise en charge ; une date de fin doit toujours être spécifiée.</li></ul>

Pour obtenir des conseils détaillés sur les exigences du compte, la configuration des autorisations et la gestion des requêtes planifiées, consultez la documentation [Plannings de requête](../ui/query-schedules.md#technical-account-user-requirements). Pour obtenir des instructions détaillées sur la création et la configuration d’un compte technique, reportez-vous aux sections [Configuration de Developer Console](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) et [Configuration de compte technique de bout en bout](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup).

## Exemples d’appels API

Une fois que vous avez configuré les en-têtes d’authentification nécessaires (voir le [guide d’authentification des API](../../landing/api-authentication.md)), vous pouvez commencer à effectuer des appels vers l’API [!DNL Query Service]. Les sections suivantes présentent divers appels API avec des formats généraux, des exemples de requêtes comprenant les en-têtes requis et des exemples de réponses.

### Récupération d’une liste de requêtes planifiées

Vous pouvez récupérer une liste de toutes les requêtes planifiées pour votre organisation en envoyant une requête GET au point d’entrée `/schedules`.

**Format d’API**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Propriété | Description |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Facultatif*) Les paramètres ajoutés au chemin de requête configurant les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les requêtes planifiées. Tous ces paramètres sont facultatifs. En effectuant un appel vers ce point d’entrée sans paramètres, vous récupérerez toutes les requêtes planifiées disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Spécifie le champ de référence pour le tri des résultats. Les champs `created` et `updated` sont pris en charge. Par exemple, `orderby=created` triera les résultats par ordre croissant de création. L’ajout d’un `-` devant created (`orderby=-created`) triera les éléments par ordre décroissant de création. |
| `limit` | Indique la limite de taille de page pour contrôler le nombre de résultats inclus dans une page. (*Valeur par défaut : 20*) |
| `start` | Spécifiez un horodatage au format ISO pour classer les résultats. Si aucune date de début n’est spécifiée, l’appel API renvoie d’abord la requête planifiée créée la plus ancienne, puis continue à répertorier les résultats les plus récents.Les horodatages ISO <br> permettent différents niveaux de granularité de la date et de l’heure. Les horodatages ISO de base prennent le format suivant : `2020-09-07` pour exprimer la date du 7 septembre 2020. Un exemple plus complexe est écrit comme `2022-11-05T08:15:30-05:00` et correspond au 5 novembre 2022, à 8 :15: 30, heure standard des États-Unis d’Amérique. Un fuseau horaire peut être fourni avec un décalage UTC et est désigné par le suffixe « Z » (`2020-01-01T01:01:01Z`). Si aucun fuseau horaire n’est fourni, la valeur par défaut est zéro. |
| `property` | Filtrez les résultats en fonction des champs. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les champs `created`, `templateId` et `userId` sont pris en charge. Les opérateurs `>` (supérieur à), `<` (inférieur à) et `==` (égal à) sont pris en charge. Par exemple, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` renvoie toutes les requêtes planifiées pour lesquelles l’identifiant utilisateur est tel qu’indiqué. |

**Requête**

La requête suivante récupère la dernière requête planifiée créée pour votre organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec une liste de requêtes planifiées pour l’organisation spécifiée. La réponse suivante renvoie la dernière requête planifiée créée pour votre organisation.

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

Vous pouvez créer une requête planifiée en effectuant une requête POST vers le point d’entrée `/schedules`. Lorsque vous créez une requête planifiée dans l’API, vous pouvez également la voir dans le Query Editor. Pour plus d’informations sur les requêtes planifiées dans l’interface utilisateur de , consultez la [documentation de Query Editor](../ui/user-guide.md#scheduled-queries).

**Format d’API**

```http
POST /schedules
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `query.dbName` | Nom de la base de données dans laquelle la requête planifiée sera exécutée. |
| `query.sql` | Requête SQL à exécuter selon le planning défini. |
| `query.name` | Le nom de la requête planifiée. |
| `query.description` | Description facultative de la requête planifiée. |
| `schedule.schedule` | Le planning cron de la requête. Reportez-vous à [Crontab.guru](https://crontab.guru/) pour une méthode interactive de création, de validation et de compréhension des expressions cron. Dans cet exemple, « 30 * * * * » signifie que la requête s’exécute toutes les heures à la 30e minute.<br><br>Vous pouvez également utiliser les expressions courtes suivantes :<ul><li>`@once` : la requête s’exécute une seule fois.</li><li>`@hourly` : la requête s’exécute toutes les heures au début de l’heure. Cela équivaut à l’expression cron `0 * * * *`.</li><li>`@daily` : la requête s’exécute une fois par jour à minuit. Cela équivaut à l’expression cron `0 0 * * *`.</li><li>`@weekly` : la requête s’exécute une fois par semaine, le dimanche, à minuit. Cela équivaut à l’expression cron `0 0 * * 0`.</li><li>`@monthly` : la requête s’exécute une fois par mois, le premier jour du mois, à minuit. Cela équivaut à l’expression cron `0 0 1 * *`.</li><li>`@yearly` : la requête s’exécute une fois par an, le 1er janvier à minuit. Cela équivaut à l’expression cron `0 0 1 1 *`. |
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

Vous pouvez récupérer des informations sur une requête planifiée spécifique en effectuant une requête GET vers le point d’entrée `/schedules` et en fournissant son identifiant dans le chemin d’accès de la requête.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Vous pouvez mettre à jour les détails d’une requête planifiée spécifiée en effectuant une requête PATCH vers le point d’entrée `/schedules` et en fournissant son identifiant dans le chemin d’accès de la requête.

La requête PATCH prend en charge deux chemins d’accès différents : `/state` et `/schedule/schedule`.

### Mise à jour de l’état de la requête planifiée

Vous pouvez mettre à jour l’état de la requête planifiée sélectionnée en définissant la propriété `path` sur `/state` et la propriété `value` sur `enable` ou `disable`.

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` de la requête planifiée que vous souhaitez PATCH. |


**Requête**

Cette requête API utilise la syntaxe du correctif JSON pour son payload. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document principes de base des API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Opération à effectuer selon le planning de requête. La valeur acceptée est `replace`. |
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

Vous pouvez mettre à jour le planning cron de la requête planifiée en définissant la propriété `path` sur `/schedule/schedule` dans le corps de la requête. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Format d’API**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` de la requête planifiée que vous souhaitez PATCH. |

**Requête**

Cette requête API utilise la syntaxe du correctif JSON pour son payload. Pour plus d’informations sur le fonctionnement du correctif JSON, consultez le document principes de base des API.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Opération à effectuer selon le planning de requête. La valeur acceptée est `replace`. |
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

Vous pouvez supprimer une requête planifiée spécifiée en effectuant une requête DELETE vers le point d’entrée `/schedules` et en fournissant l’identifiant de la requête planifiée que vous souhaitez supprimer du chemin d’accès de la requête.

>[!NOTE]
>
>Le planning **doit** doit être désactivé avant d’être supprimé.

**Format d’API**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` de la requête planifiée que vous souhaitez DELETE. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
