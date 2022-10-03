---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;alerte;
title: Point de terminaison de l’API des abonnements des alertes
description: Ce guide fournit des exemples de requêtes et de réponses HTTP pour les différents appels API que vous pouvez effectuer au point de terminaison des abonnements aux alertes avec l’API Query Service.
source-git-commit: cab7fcfda1bd8f6462af6e631f1fcee1f354d26b
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 5%

---

# Point de terminaison de l’API des abonnements des alertes

Adobe Experience Platform Query Service vous permet de vous abonner à des alertes pour les requêtes ad hoc et planifiées. Les alertes peuvent être reçues par courrier électronique, dans l’interface utilisateur de Platform ou les deux. Le contenu de la notification est le même pour les alertes in-Platform et les alertes par email. Actuellement, les alertes de requête ne peuvent être abonnées qu’à l’aide de la variable [API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Pour recevoir des alertes par courrier électronique, vous devez d’abord activer ce paramètre dans l’interface utilisateur. Consultez la documentation pour [instructions pour activer les alertes par email](../../observability/alerts/ui.md#enable-email-alerts).

Le tableau ci-dessous décrit les types d’alerte pris en charge pour différents types de requêtes :

| Type de requête | Types d’alerte pris en charge |
|---|---|
| Requêtes ad hoc | `success` ou `failed` exécutions. |
| Requêtes planifiées | `start`, `success`ou `failed` exécutions. |

>[!NOTE]
>
>Toutes les requêtes non SELECT prennent en charge les abonnements aux alertes et vous n’avez pas besoin d’être le créateur de requêtes pour vous abonner à une alerte. D’autres utilisateurs peuvent également s’inscrire aux alertes d’une requête qu’ils n’ont pas créée.

Les alertes suivantes s’appliquent sans abonnement aux alertes :

* Une fois la tâche de requête par lots terminée, les utilisateurs reçoivent une notification.
* Lorsque la durée d’une tâche de requête par lot dépasse un seuil, une alerte est déclenchée à la personne qui a planifié la requête.

>[!NOTE]
>
>Les requêtes utilisées pour les tests peuvent être exclues de ces alertes si elles sont correctement configurées.

## Exemples d’appels API

Les sections suivantes décrivent les différents appels API que vous pouvez effectuer à l’aide de l’API Query Service. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

## Récupération d’une liste de toutes les alertes pour une organisation et un environnement de test {#get-list-of-org-alert-subs}

Récupérez une liste de toutes les alertes d’un environnement de test d’organisation en envoyant une requête GET à la variable `/alert-subscriptions` point de terminaison .

**Format d’API**

```http
GET /alert-subscriptions
```

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 et le `alerts` tableau avec pagination et informations sur la version. Le `alerts` contient les détails de toutes les alertes pour une organisation et un environnement de test spécifique. Au maximum trois alertes sont disponibles par réponse, une alerte par type d’alerte est contenue dans le corps de la réponse.

>[!NOTE]
>
>Le `alerts._links` dans le `alerts` a été tronquée pour la concision. Un exemple complet de la fonction `alerts._links` se trouve dans la variable [réponse de la demande du POST](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Propriété | Description |
| -------- | ----------- |
| `alerts.assetId` | Identifiant de requête qui a associé l’alerte à une requête spécifique. |
| `alerts.id` | Nom de l’alerte. Ce nom est généré par le service Alertes et utilisé dans le tableau de bord Alertes . Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType`et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la section [Documentation du tableau de bord Alertes Platform](../../observability/alerts/ui.md). |
| `alerts.status` | L’alerte a quatre valeurs d’état : `enabled`, `enabling`, `disabled`, et `disabling`. Une alerte écoute activement les événements, est suspendue pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres appropriés, ou est en transition entre ces états. |
| `alerts.alertType` | Type d’alerte. Une alerte peut avoir trois valeurs : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `alerts._links` | Fournit des informations sur les méthodes et points de terminaison disponibles qui peuvent être utilisés pour récupérer, mettre à jour, modifier ou supprimer des informations relatives à cet identifiant d’alerte. |
| `_page` | L’objet contient des propriétés pour décrire l’ordre, la taille, le nombre total de pages et la page active. |
| `_links` | L’objet contient des références URI qui peuvent être utilisées pour obtenir la page de ressources suivante ou précédente. |

## Récupération des informations d’abonnement aux alertes pour une requête ou un ID de planification spécifique {#retrieve-all-alert-subscriptions-by-id}

Récupérez les informations d’abonnement à l’alerte pour un ID de requête ou un ID de planification spécifique en envoyant une requête GET à la variable `/alert-subscriptions/{QUERY_ID}` ou le `/alert-subscriptions/{SCHEDULE_ID}` point de terminaison .

**Format d’API**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{QUERY_ID}` | L’identifiant de la requête pour laquelle vous souhaitez renvoyer les informations d’abonnement. |
| `{SCHEDULE_ID}` | L’identifiant de la requête planifiée pour laquelle vous souhaitez renvoyer les informations d’abonnement. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP de 200 et l’événement `alerts` tableau contenant les informations d’abonnement pour l’ID de requête ou de planification fourni.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `assetId` | L’alerte est associée à cet identifiant. L’ID peut être un ID de requête ou un ID de planification. |
| `id` | Nom de l’alerte. Ce nom est généré par le service Alertes et utilisé dans le tableau de bord Alertes . Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType`et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la section [Documentation du tableau de bord Alertes Platform](../../observability/alerts/ui.md). |
| `status` | L’alerte a quatre valeurs d’état : `enabled`, `enabling`, `disabled`, et `disabling`. Une alerte écoute activement les événements, est suspendue pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres appropriés, ou est en transition entre ces états. |
| `alertType` | Chaque alerte peut avoir trois types d’alerte différents. Ils sont : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `subscriptions.emailNotifications` | Tableau d’adresses électroniques enregistrées par l’Adobe pour les utilisateurs qui se sont abonnés pour recevoir des courriers électroniques pour l’alerte. |
| `subscriptions.inContextNotifications` | Tableau d’adresses électroniques enregistrées par l’Adobe pour les utilisateurs qui se sont abonnés aux notifications de l’interface utilisateur pour l’alerte. |

## Récupération des informations d’abonnement aux alertes pour une requête ou un ID de planification et un type d’alerte spécifiques {#get-alert-info-by-id-and-alert-type}

Récupérez les informations d’abonnement à l’alerte pour un identifiant et un type d’alerte spécifiques en adressant une requête GET à la variable `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` point de terminaison . Cela s’applique aux ID de requête ou aux ID de requête planifiés.

**Format d’API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Paramètres | Description |
| -------- | ----------- |
| `ALERT_TYPE` | Chaque alerte peut avoir trois types d’alerte différents. Ils sont : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `QUERY_ID` | Identifiant unique de la requête à mettre à jour. |
| `SCHEDULE_ID` | Identifiant unique de la requête planifiée à mettre à jour. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP de 200 et toutes les alertes auxquelles vous êtes abonné. Il s’agit notamment de l’identifiant de l’alerte, du type d’alerte, des identifiants d’adresse électronique enregistrés de l’Adobe de l’abonné et de leur canal de notification préféré.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `assetId` | Identifiant de requête qui a associé l’alerte à une requête spécifique. |
| `alertType` | Type d’alerte. Une alerte peut avoir trois valeurs : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `subscriptions` | Objet utilisé pour transmettre les ID d’email enregistrés par l’Adobe associés aux alertes, ainsi que les canaux dans lesquels les utilisateurs recevront les alertes. |
| `subscriptions.inContextNotifications` | Tableau d’adresses électroniques enregistrées par l’Adobe pour les utilisateurs qui se sont abonnés aux notifications de l’interface utilisateur pour l’alerte. |
| `subscriptions.emailNotifications` | Tableau d’adresses électroniques enregistrées par l’Adobe pour les utilisateurs qui se sont abonnés pour recevoir des courriers électroniques pour l’alerte. |

## Récupérer une liste de toutes les alertes auxquelles un utilisateur est abonné {#get-alert-subscription-list}

Récupérez la liste de toutes les alertes auxquelles un utilisateur est abonné en adressant une requête GET à la fonction `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` point de terminaison . La réponse inclut le nom de l’alerte, les identifiants, l’état, le type d’alerte et les canaux de notification.

**Format d’API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Paramètres | Description |
| -------- | ----------- |
| `{EMAIL_ID}` | Adresse électronique enregistrée dans un compte Adobe permettant d’identifier les utilisateurs abonnés aux alertes. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 et le `items` tableau avec les détails des alertes auxquelles sont abonnés les `emailId` fourni.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de l’alerte. Ce nom est généré par le service Alertes et utilisé dans le tableau de bord Alertes . Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType`et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la section [Documentation du tableau de bord Alertes Platform](../../observability/alerts/ui.md). |
| `assetId` | Identifiant de requête qui a associé l’alerte à une requête spécifique. |
| `status` | L’alerte a quatre valeurs d’état : `enabled`, `enabling`, `disabled`, et `disabling`. Une alerte écoute activement les événements, est suspendue pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres appropriés, ou est en transition entre ces états. |
| `alertType` | Type d’alerte. Une alerte peut avoir trois valeurs : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `subscriptions` | Objet utilisé pour transmettre les ID d’email enregistrés par l’Adobe associés aux alertes, ainsi que les canaux dans lesquels les utilisateurs recevront les alertes. |
| `subscriptions.inContextNotifications` | Valeur boolean qui détermine la manière dont les utilisateurs reçoivent les notifications d’alerte. A `true` confirme que les alertes doivent être fournies via l’interface utilisateur. A `false` garantit que les utilisateurs ne sont pas avertis via ce canal. |
| `subscriptions.emailNotifications` | Valeur boolean qui détermine la manière dont les utilisateurs reçoivent les notifications d’alerte. A `true` confirme que les alertes doivent être fournies par email. A `false` garantit que les utilisateurs ne sont pas avertis via ce canal. |

## Créer une alerte et abonner des utilisateurs {#subscribe-users}

Pour créer une alerte et abonner un utilisateur à la recevoir, effectuez une `POST` à la fonction `/alert-subscriptions` point de terminaison . Cette requête associe une requête à une alerte nouvellement créée à l’aide d’une `assetId` et abonne les utilisateurs aux alertes pour cette requête au moyen de l’option `emailIds`.

>[!IMPORTANT]
>
>Vous pouvez transmettre jusqu’à cinq ID d’adresse électronique enregistrés par Adobe dans une seule requête. Pour abonner plus de cinq utilisateurs à une alerte, des requêtes ultérieures doivent être effectuées.

**Format d’API**

```http
POST /alert-subscriptions
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `assetId` | L’alerte est associée à cet identifiant. L’ID peut être un ID de requête ou un ID de planification. |
| `alertType` | Type d’alerte. Une alerte peut avoir trois valeurs : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `subscriptions` | Objet utilisé pour transmettre les ID d’email enregistrés par l’Adobe associés aux alertes, ainsi que les canaux dans lesquels les utilisateurs recevront les alertes. |
| `subscriptions.emailIds` | Tableau d’adresses électroniques permettant d’identifier les utilisateurs qui doivent recevoir les alertes. Les adresses électroniques **must** être enregistré sur un compte Adobe. |
| `subscriptions.inContextNotifications` | Valeur boolean qui détermine la manière dont les utilisateurs reçoivent les notifications d’alerte. A `true` confirme que les alertes doivent être fournies via l’interface utilisateur. A `false` garantit que les utilisateurs ne sont pas avertis via ce canal. |
| `subscriptions.emailNotifications` | Valeur boolean qui détermine la manière dont les utilisateurs reçoivent les notifications d’alerte. A `true` confirme que les alertes doivent être fournies par email. A `false` garantit que les utilisateurs ne sont pas avertis via ce canal. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (Accepted) avec les détails de votre nouvelle alerte.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Nom de l’alerte. Ce nom est généré par le service Alertes et utilisé dans le tableau de bord Alertes . Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType`et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la section [Documentation du tableau de bord Alertes Platform](../../observability/alerts/ui.md). |
| `_links` | Fournit des informations sur les méthodes et points de terminaison disponibles qui peuvent être utilisés pour récupérer, mettre à jour, modifier ou supprimer des informations relatives à cet identifiant d’alerte. |

## Activation ou désactivation d’une alerte {#enable-or-disable-alert}

Cette requête fait référence à une alerte spécifique à l’aide d’un identifiant de requête ou de planification et d’un type d’alerte, puis met à jour l’état de l’alerte en `enable` ou `disable`. Vous pouvez mettre à jour l’état d’une alerte en effectuant une `PATCH` à la fonction `/alert-subscriptions/{queryId}/{alertType}` ou `/alert-subscriptions/{scheduleId}/{alertType}` point de terminaison .

**Format d’API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Paramètres | Description |
| -------- | ----------- |
| `ALERT_TYPE` | Type d’alerte. Une alerte peut avoir trois valeurs : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul>Vous devez spécifier le type d’alerte actuel dans l’espace de noms du point de terminaison pour le modifier. |
| `QUERY_ID` | Identifiant unique de la requête à mettre à jour. |
| `SCHEDULE_ID` | Identifiant unique de la requête planifiée à mettre à jour. |

**Requête**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `op` | Opération à effectuer. Actuellement, la seule valeur acceptée est `replace`. |
| `path` | Cette valeur correspond à l’espace de noms du point de terminaison . Actuellement, la seule valeur acceptée est `/status`. |
| `value` | Dans une requête de PATCH réussie, cela modifie la variable `status` valeur de l’alerte. Actuellement, les valeurs acceptées sont `enable` ou `disable`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de l’état, du type et de l’identifiant de l’alerte, ainsi que la requête à laquelle elle se rapporte.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Nom de l’alerte. Ce nom est généré par le service Alertes et utilisé dans le tableau de bord Alertes . Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType`et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la section [Documentation du tableau de bord Alertes Platform](../../observability/alerts/ui.md). |
| `assetId` | L’alerte est associée à cet identifiant. L’ID peut être un ID de requête ou un ID de planification. |
| `alertType` | Chaque alerte peut avoir trois types d’alerte différents. Ils sont : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> |
| `status` | L’alerte a quatre valeurs d’état : `enabled`, `enabling`, `disabled`, et `disabling`. Une alerte écoute activement les événements, est suspendue pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres appropriés, ou est en transition entre ces états. |

## Supprimer l’alerte d’une requête et d’un type d’alerte spécifiques {#delete-alert-info-by-id-and-alert-type}

Supprimez une alerte pour une requête ou un ID de planification et un type d’alerte spécifiques en adressant une requête de DELETE à la fonction `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` ou `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` point de terminaison .

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Paramètres | Description |
| -------- | ----------- |
| `ALERT_TYPE` | Type d’alerte. Une alerte peut avoir trois valeurs : <ul><li>`start`: Avertit un utilisateur lorsque l’exécution de la requête a commencé.</li><li>`success`: Avertit l’utilisateur une fois la requête terminée.</li><li>`failure`: Avertit l’utilisateur en cas d’échec de la requête.</li></ul> La demande du DELETE s’applique uniquement au type d’alerte spécifique fourni. |
| `QUERY_ID` | Identifiant unique de la requête à mettre à jour. |
| `SCHEDULE_ID` | Identifiant unique de la requête planifiée à mettre à jour. |

**Requête**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 et un message de confirmation incluant l’identifiant de la ressource et le type d’alerte de l’alerte supprimée.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Étapes suivantes

Ce guide décrit l’utilisation de la variable `/alert-subscriptions` point d’entrée dans l’API Query Service. Après avoir lu ce guide, vous comprenez mieux comment créer une alerte pour une requête, abonner les utilisateurs à l’alerte, les types d’alertes disponibles et comment récupérer, mettre à jour et supprimer des informations d’abonnement aux alertes.

Voir [Guide de l’API Query Service](./getting-started.md) pour en savoir plus sur les autres fonctionnalités et opérations disponibles.
