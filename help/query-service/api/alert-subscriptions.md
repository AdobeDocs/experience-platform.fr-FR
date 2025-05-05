---
keywords: Experience Platform;accueil;rubriques populaires;Query Service;Query Service;alert;
title: Point D’Entrée Des Abonnements Aux Alertes
description: Ce guide fournit des exemples de requêtes et de réponses HTTP pour les différents appels API que vous pouvez effectuer au point d’entrée des abonnements aux alertes avec l’API Query Service.
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3217'
ht-degree: 68%

---

# Point d’entrée des abonnements aux alertes

Adobe Experience Platform Query Service vous permet de vous abonner à des alertes pour les requêtes ad hoc et planifiées. Les alertes peuvent être reçues par e-mail, dans l’interface utilisateur d’Experience Platform ou les deux. Le contenu de la notification est le même pour les alertes dans Experience Platform et les alertes par e-mail.

## Commencer

Les points d’entrée utilisés dans ce guide font partie de l’API Adobe Experience Platform [Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/). Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

>[!IMPORTANT]
>
>Pour recevoir des alertes par e-mail, vous devez d’abord activer ce paramètre dans l’interface utilisateur. Consultez la documentation pour des [instructions sur la façon d’activer les alertes par e-mail](../../observability/alerts/ui.md#enable-email-alerts).

## Types d’alerte {#alert-types}

Le tableau ci-dessous décrit les types d’alerte de requête pris en charge :

>[!IMPORTANT]
>
>Le type d’alerte `delay` ou [!UICONTROL Délai d’exécution de requête] n’est actuellement pas pris en charge par l’API Query Service. Cette alerte vous avertit en cas de retard dans le résultat d’une exécution de requête planifiée au-delà d’un seuil spécifié. Pour utiliser cette alerte, vous devez définir une heure personnalisée qui déclenche une alerte lorsque la requête s’exécute pendant cette durée sans terminer ni échouer. Pour savoir comment définir cette alerte dans l’interface utilisateur, reportez-vous à la documentation [plannings de requête](../ui/query-schedules.md#alerts-for-query-status) ou au [guide des actions de requête intégrées](../ui/monitor-queries.md#query-run-delay).

| Type d’alerte | Description |
|---|---|
| `start` | Cette alerte vous avertit lorsqu’une exécution de requête planifiée est lancée ou commence à être traitée. |
| `success` | Cette alerte vous informe lorsqu’une exécution de requête planifiée se termine avec succès, indiquant que la requête s’est exécutée sans erreur. |
| `failed` | Cette alerte se déclenche lorsqu’une exécution de requête planifiée rencontre une erreur ou ne s’exécute pas correctement. Cela vous aide à identifier et à résoudre les problèmes rapidement. |
| `quarantine` | Cette alerte est activée lorsqu’une exécution de requête planifiée est mise en quarantaine. Lorsque des requêtes sont inscrites dans la fonction de quarantaine, toute requête planifiée qui échoue dix exécutions consécutives est automatiquement placée dans un état [!UICONTROL Quarantaine]. Elles nécessitent ensuite votre intervention avant que d’autres exécutions ne puissent avoir lieu. |

>[!NOTE]
>
>Toutes les requêtes sauf les requêtes SELECT prennent en charge les abonnements aux alertes, et il n’est pas nécessaire d’être le créateur de la requête pour s’abonner à une alerte. D’autres utilisateurs et utilisatrices peuvent également s’inscrire pour recevoir des alertes sur une requête qu’ils n’ont pas créée.

Les alertes suivantes s’appliquent sans abonnement aux alertes :

* Lorsqu’un traitement de requêtes par lots se termine, les utilisateurs et utilisatrices reçoivent une notification.
* Lorsque la durée d’un traitement de requête par lots dépasse un seuil, une alerte est déclenchée à l’attention de la personne qui a planifié la requête.

>[!NOTE]
>
>Les requêtes utilisées pour les tests peuvent être exclues de ces alertes si elles sont configurées de manière appropriée.

## Exemples d’appels API

Les sections suivantes décrivent les différents appels API que vous pouvez effectuer à l’aide de l’API Query Service. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

## Récupérer une liste de toutes les alertes pour une organisation et un sandbox {#get-list-of-org-alert-subs}

Récupérer une liste de toutes les alertes pour un sandbox d’organisation en envoyant une requête GET au point d’entrée `/alert-subscriptions`.

**Format d’API**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| Propriété | Description |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | (Facultatif) Paramètres ajoutés au chemin d’accès de la requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (&amp;). Les paramètres disponibles sont répertoriés ci-dessous. |

**Paramètres de requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour répertorier les requêtes. Tous ces paramètres sont facultatifs. En effectuant un appel vers ce point d’entrée sans paramètres, vous récupérerez toutes les requêtes disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `orderby` | Champ spécifiant l’ordre des résultats. Les champs `created` et `updated` sont pris en charge. Ajoutez le nom de la propriété avec le `+` pour l’ordre croissant et le `-` pour l’ordre décroissant. La valeur par défaut est `-created`. Notez que le signe plus (`+`) doit être placé dans une séquence d’échappement avec `%2B`. Par exemple, `%2Bcreated` est la valeur d’une commande créée ascendante. |
| `pagesize` | Utilisez ce paramètre pour contrôler le nombre d’enregistrements que vous souhaitez récupérer à partir de l’appel API par page. La limite par défaut est définie sur la quantité maximale de 50 enregistrements par page. |
| `page` | Indiquez le numéro de page des résultats renvoyés pour lesquels vous souhaitez afficher les enregistrements. |
| `property` | Filtrez les résultats en fonction des champs sélectionnés. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les propriétés suivantes permettent le filtrage : <ul><li>identifiant</li><li>assetId</li><li>statut</li><li>alertType</li></ul> Les opérateurs pris en charge sont `==` (égal à). Par exemple, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` renverra l’alerte avec un identifiant correspondant. |

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

Une réponse réussie renvoie un état HTTP 200 et le tableau `alerts` avec les informations de pagination et de version. Le tableau `alerts` contient les détails de toutes les alertes pour une organisation et un sandbox spécifique. Trois alertes au maximum sont disponibles par réponse, une alerte par type d’alerte est contenue dans le corps de la réponse.

>[!NOTE]
>
>L’objet `alerts._links` dans le tableau `alerts` a été tronqué par souci de concision. Un exemple complet de l’objet `alerts._links` se trouve dans la [réponse de la requête POST](#subscribe-users).

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
| `alerts.assetId` | L’identifiant de la requête qui a associé l’alerte à une requête spécifique. |
| `alerts.id` | Nom de l’alerte. Ce nom est généré par le service d’alertes et est utilisé sur le tableau de bord des alertes. Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType` et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la documentation du tableau de bord des alertes Experience Platform [&#128279;](../../observability/alerts/ui.md). |
| `alerts.status` | L’alerte a quatre valeurs de statut : `enabled`, `enabling`, `disabled` et `disabling`. Une alerte écoute activement les événements, est mise en pause pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres pertinents, ou passe d’un état à l’autre. |
| `alerts.alertType` | Le type d’alerte. Cinq états d’alerte sont disponibles pour les requêtes planifiées, bien que seuls quatre états d’alerte soient disponibles pour les requêtes ad hoc. L’alerte `quarantine` n’est disponible que pour les requêtes planifiées. En outre, vous ne pouvez définir l’alerte `delay` qu’à partir de l’interface utilisateur d’Experience Platform. Pour cette raison, `delay` n&#39;est pas décrit ici. Les alertes disponibles sont les suivantes : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li><li>`quarantine` : s’active lorsqu’une exécution de requête planifiée est mise en quarantaine.</li></ul> |
| `alerts._links` | Fournit des informations sur les méthodes et points d’entrée disponibles qui peuvent être utilisés pour récupérer, mettre à jour, modifier ou supprimer des informations relatives à cet identifiant d’alerte. |
| `_page` | L’objet contient des propriétés pour décrire l’ordre, la taille, le nombre total de pages et la page active. |
| `_links` | L’objet contient des références URI qui peuvent être utilisées pour obtenir la page de ressources suivante ou précédente. |

## Récupérer les informations sur l’abonnement aux alertes pour une requête ou un identifiant de planning spécifiques {#retrieve-all-alert-subscriptions-by-id}

Récupérez les informations sur l’abonnement aux alertes pour un identifiant de requête ou un identifiant de planning spécifiques en envoyant une requête GET au point d’entrée `/alert-subscriptions/{QUERY_ID}` ou `/alert-subscriptions/{SCHEDULE_ID}`.

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

Une réponse réussie renvoie un état HTTP de 200 et le tableau `alerts` qui contient les informations d’abonnement pour l’identifiant de requête ou de planning fourni.

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
| `assetId` | L’alerte est associée à cet identifiant. L’ID peut être un ID de requête ou un ID de planning. |
| `id` | Nom de l’alerte. Ce nom est généré par le service d’alertes et est utilisé sur le tableau de bord des alertes. Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType` et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la documentation du tableau de bord des alertes Experience Platform [&#128279;](../../observability/alerts/ui.md). |
| `status` | L’alerte a quatre valeurs de statut : `enabled`, `enabling`, `disabled` et `disabling`. Une alerte écoute activement les événements, est mise en pause pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres pertinents, ou passe d’un état à l’autre. |
| `alertType` | Chaque alerte peut avoir trois types d’alerte différents. Les voici : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li></ul> |
| `subscriptions.emailNotifications` | Tableau d’adresses électroniques enregistrées par Adobe pour les utilisateurs et utilisatrices qui se sont abonnés pour recevoir des e-mails pour l’alerte. |
| `subscriptions.inContextNotifications` | Tableau d’adresses électroniques enregistrées par Adobe pour les utilisateurs et utilisatrices qui sont abonnés aux notifications de l’interface utilisateur pour l’alerte. |

## Récupération d’informations relatives à l’abonnement aux alertes pour un ID de requête ou de planning et un type d’alerte spécifiques {#get-alert-info-by-id-and-alert-type}

Récupérez des informations relatives à l’abonnement aux alertes pour un ID et un type d’alerte spécifique en envoyant une requête GET au point d’entrée `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}`. Cela s’applique à la fois aux ID de requêtes et aux ID de requêtes planifiées.

**Format d’API**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Paramètres | Description |
| -------- | ----------- |
| `ALERT_TYPE` | Cette propriété décrit le statut d’exécution de la requête qui déclenche une alerte. La réponse inclut uniquement les informations relatives à l’abonnement aux alertes pour les alertes de ce type. Chaque alerte peut avoir trois types d’alerte différents. Les voici : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li></ul> |
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

Une réponse réussie renvoie un statut HTTP de 200 et toutes les alertes auxquelles vous êtes abonné. Il s’agit notamment de l’identifiant de l’alerte, du type d’alerte, des identifiants d’adresse électronique enregistrée par Adobe et du canal de notification préféré de l’abonné.

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
| `assetId` | L’identifiant de la requête qui a associé l’alerte à une requête spécifique. |
| `alertType` | Le type d’alerte. Cinq états d’alerte sont disponibles pour les requêtes planifiées, bien que seuls quatre états d’alerte soient disponibles pour les requêtes ad hoc. L’alerte `quarantine` n’est disponible que pour les requêtes planifiées. En outre, vous ne pouvez définir l’alerte `delay` qu’à partir de l’interface utilisateur d’Experience Platform. Pour cette raison, `delay` n&#39;est pas décrit ici. Les alertes disponibles sont les suivantes : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li><li>`quarantine` : s’active lorsqu’une exécution de requête planifiée est mise en quarantaine.</li></ul> |
| `subscriptions` | Objet utilisé pour transmettre les identifiants d’adresse électronique enregistrée par Adobe associés aux alertes, ainsi que les canaux via lesquels les utilisateurs et utilisatrices recevront les alertes. |
| `subscriptions.inContextNotifications` | Tableau d’adresses électroniques enregistrées par Adobe pour les utilisateurs et utilisatrices qui sont abonnés aux notifications de l’interface utilisateur pour l’alerte. |
| `subscriptions.emailNotifications` | Tableau d’adresses électroniques enregistrées par Adobe pour les utilisateurs et utilisatrices qui se sont abonnés pour recevoir des e-mails pour l’alerte. |

## Récupération d’une liste de toutes les alertes auxquelles un utilisateur ou une utilisatrice est abonné {#get-alert-subscription-list}

Récupérez une liste de toutes les alertes auxquelles un utilisateur ou une utilisatrice est abonné en adressant une requête GET au point d’entrée `/alert-subscriptions/user-subscriptions/{EMAIL_ID}`. La réponse inclut le nom de l’alerte, les identifiants, le statut, le type d’alerte et les canaux de notification.

**Format d’API**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Paramètres | Description |
| -------- | ----------- |
| `{EMAIL_ID}` | Adresse électronique enregistrée dans un compte Adobe permettant d’identifier les utilisateurs et utilisatrices abonnés aux alertes. |
| `orderby` | Champ spécifiant l’ordre des résultats. Les champs `created` et `updated` sont pris en charge. Ajoutez le nom de la propriété avec le `+` pour l’ordre croissant et le `-` pour l’ordre décroissant. La valeur par défaut est `-created`. Notez que le signe plus (`+`) doit être placé dans une séquence d’échappement avec `%2B`. Par exemple, `%2Bcreated` est la valeur d’une commande créée ascendante. |
| `pagesize` | Utilisez ce paramètre pour contrôler le nombre d’enregistrements que vous souhaitez récupérer à partir de l’appel API par page. La limite par défaut est définie sur la quantité maximale de 50 enregistrements par page. |
| `page` | Indiquez le numéro de page des résultats renvoyés pour lesquels vous souhaitez afficher les enregistrements. |
| `property` | Filtrez les résultats en fonction des champs sélectionnés. Les filtres **doivent** être précédés d’une séquence d’échappement HTML. Des virgules sont utilisées pour combiner plusieurs ensembles de filtres. Les propriétés suivantes permettent le filtrage : <ul><li>identifiant</li><li>assetId</li><li>statut</li><li>alertType</li></ul> Les opérateurs pris en charge sont `==` (égal à). Par exemple, `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` renverra l’alerte avec un identifiant correspondant. |

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

Une réponse réussie renvoie un statut HTTP 200 et le tableau `items` avec les détails des alertes auxquelles sont abonnés les `emailId` fournis.

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
| `name` | Nom de l’alerte. Ce nom est généré par le service d’alertes et est utilisé sur le tableau de bord des alertes. Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType` et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la documentation du tableau de bord des alertes Experience Platform [&#128279;](../../observability/alerts/ui.md). |
| `assetId` | L’identifiant de la requête qui a associé l’alerte à une requête spécifique. |
| `status` | L’alerte a quatre valeurs de statut : `enabled`, `enabling`, `disabled` et `disabling`. Une alerte écoute activement les événements, est mise en pause pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres pertinents, ou passe d’un état à l’autre. |
| `alertType` | Le type d’alerte. Cinq états d’alerte sont disponibles pour les requêtes planifiées, bien que seuls quatre états d’alerte soient disponibles pour les requêtes ad hoc. L’alerte `quarantine` n’est disponible que pour les requêtes planifiées. En outre, vous ne pouvez définir l’alerte `delay` qu’à partir de l’interface utilisateur d’Experience Platform. Pour cette raison, `delay` n&#39;est pas décrit ici. Les alertes disponibles sont les suivantes : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li><li>`quarantine` : s’active lorsqu’une exécution de requête planifiée est mise en quarantaine.</li></ul> |
| `subscriptions` | Objet utilisé pour transmettre les identifiants d’adresse électronique enregistrée par Adobe associés aux alertes, ainsi que les canaux via lesquels les utilisateurs et utilisatrices recevront les alertes. |
| `subscriptions.inContextNotifications` | Valeur booléenne déterminant la manière dont les utilisateurs et utilisatrices reçoivent les notifications d’alerte. Une valeur `true` confirme que les alertes doivent être fournies via l’interface utilisateur. Une valeur `false` garantit que les utilisateurs et utilisatrices ne sont pas avertis par ce canal. |
| `subscriptions.emailNotifications` | Valeur booléenne déterminant la manière dont les utilisateurs et utilisatrices reçoivent les notifications d’alerte. Une valeur `true` confirme que les alertes doivent être fournies par e-mail. Une valeur `false` garantit que les utilisateurs et utilisatrices ne sont pas avertis par ce canal. |

## Création d’une alerte et abonnement des utilisateurs {#subscribe-users}

Pour créer une alerte et y abonner un utilisateur ou une utilisatrice, adressez une requête `POST` au point d’entrée `/alert-subscriptions`. Cette demande associe une requête à une alerte nouvellement créée à l’aide d’une propriété `assetId`, et abonne les utilisateurs et utilisatrices aux alertes de cette requête grâce à l’utilisation des `emailIds`.

>[!IMPORTANT]
>
>Vous pouvez transmettre jusqu’à cinq identifiants d’e-mail enregistrés par Adobe en une seule requête. Pour abonner plus de cinq utilisateurs ou utilisatrices à une alerte, des requêtes ultérieures doivent être adressées.

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
| `assetId` | L’alerte est associée à cet identifiant. L’ID peut être un ID de requête ou un ID de planning. |
| `alertType` | Le type d’alerte. Cinq états d’alerte sont disponibles pour les requêtes planifiées, bien que seuls quatre états d’alerte soient disponibles pour les requêtes ad hoc. L’alerte `quarantine` n’est disponible que pour les requêtes planifiées. En outre, vous ne pouvez définir l’alerte `delay` qu’à partir de l’interface utilisateur d’Experience Platform. Pour cette raison, `delay` n&#39;est pas décrit ici. Les alertes disponibles sont les suivantes : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li><li>`quarantine` : s’active lorsqu’une exécution de requête planifiée est mise en quarantaine.</li></ul> |
| `subscriptions` | Objet utilisé pour transmettre les identifiants d’adresse électronique enregistrée par Adobe associés aux alertes, ainsi que les canaux via lesquels les utilisateurs et utilisatrices recevront les alertes. |
| `subscriptions.emailIds` | Un tableau d’adresses e-mail pour identifier les utilisateurs et utilisatrices qui doivent recevoir les alertes. Les adresses e-mail **doivent** être enregistrées sur un compte Adobe. |
| `subscriptions.inContextNotifications` | Valeur booléenne déterminant la manière dont les utilisateurs et utilisatrices reçoivent les notifications d’alerte. Une valeur `true` confirme que les alertes doivent être fournies via l’interface utilisateur. Une valeur `false` garantit que les utilisateurs et utilisatrices ne sont pas avertis par ce canal. |
| `subscriptions.emailNotifications` | Valeur booléenne déterminant la manière dont les utilisateurs et utilisatrices reçoivent les notifications d’alerte. Une valeur `true` confirme que les alertes doivent être fournies par e-mail. Une valeur `false` garantit que les utilisateurs et utilisatrices ne sont pas avertis par ce canal. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie le statut HTTP 202 (Accepté) avec les détails de votre alerte nouvellement créée.

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
| `id` | Nom de l’alerte. Ce nom est généré par le service d’alertes et est utilisé sur le tableau de bord des alertes. Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType` et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la documentation du tableau de bord des alertes Experience Platform [&#128279;](../../observability/alerts/ui.md). |
| `_links` | Fournit des informations sur les méthodes et points d’entrée disponibles qui peuvent être utilisés pour récupérer, mettre à jour, modifier ou supprimer des informations relatives à cet identifiant d’alerte. |

## Activer ou désactiver une alerte {#enable-or-disable-alert}

Cette requête fait référence à une alerte spécifique à l’aide d’un identifiant de requête ou de planning et d’un type d’alerte, puis met à jour l’état de l’alerte en `enable` ou `disable`. Vous pouvez mettre à jour le statut d’une alerte en adressant une requête `PATCH` au point d’entrée `/alert-subscriptions/{queryId}/{alertType}` ou `/alert-subscriptions/{scheduleId}/{alertType}`.

**Format d’API**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Paramètres | Description |
| -------- | ----------- |
| `ALERT_TYPE` | Le type d’alerte. Cinq états d’alerte sont disponibles pour les requêtes planifiées, bien que seuls quatre états d’alerte soient disponibles pour les requêtes ad hoc. L’alerte `quarantine` n’est disponible que pour les requêtes planifiées. En outre, vous ne pouvez définir l’alerte `delay` qu’à partir de l’interface utilisateur d’Experience Platform. Pour cette raison, `delay` n&#39;est pas décrit ici. Les alertes disponibles sont les suivantes : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li><li>`quarantine` : s’active lorsqu’une exécution de requête planifiée est mise en quarantaine.</li></ul>Vous devez spécifier le type d’alerte actuel dans l’espace de noms du point d’entrée afin de le modifier. |
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
| `path` | Cette valeur concerne l’espace de nom dans le point d’entrée. Actuellement, la seule valeur acceptée est `/status`. |
| `value` | Dans une requête PATCH réussie, cela modifie la valeur `status` de l’alerte. Actuellement, les valeurs acceptées sont `enable` ou `disable`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec des détails sur le statut, le type et l’identifiant de l’alerte ainsi que la requête à laquelle elle se rapporte.

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
| `id` | Nom de l’alerte. Ce nom est généré par le service d’alertes et est utilisé sur le tableau de bord des alertes. Le nom de l’alerte comprend le dossier dans lequel l’alerte est stockée, le `alertType` et l’ID de flux. Vous trouverez des informations sur les alertes disponibles dans la documentation du tableau de bord des alertes Experience Platform [&#128279;](../../observability/alerts/ui.md). |
| `assetId` | L’alerte est associée à cet identifiant. L’ID peut être un ID de requête ou un ID de planning. |
| `alertType` | Chaque alerte peut avoir trois types d’alerte différents. Les voici : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li></ul> |
| `status` | L’alerte a quatre valeurs de statut : `enabled`, `enabling`, `disabled`, et `disabling`. Une alerte écoute activement les événements, est mise en pause pour une utilisation ultérieure tout en conservant tous les abonnés et paramètres pertinents, ou passe d’un état à l’autre. |

## Supprimer l’alerte d’une requête et d’un type d’alerte spécifiques {#delete-alert-info-by-id-and-alert-type}

Supprimez une alerte pour un identifiant de requête ou de planning et un type d’alerte spécifiques en adressant une requête DELETE au point d’entrée `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` ou `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}`.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Paramètres | Description |
| -------- | ----------- |
| `ALERT_TYPE` | Le type d’alerte. Cinq états d’alerte sont disponibles pour les requêtes planifiées, bien que seuls quatre états d’alerte soient disponibles pour les requêtes ad hoc. L’alerte `quarantine` n’est disponible que pour les requêtes planifiées. En outre, vous ne pouvez définir l’alerte `delay` qu’à partir de l’interface utilisateur d’Experience Platform. Pour cette raison, `delay` n&#39;est pas décrit ici. Les alertes disponibles sont les suivantes : <ul><li>`start` : avertit un utilisateur ou une utilisatrice du démarrage de l’exécution de la requête.</li><li>`success` : avertit l’utilisateur ou l’utilisatrice une fois la requête terminée.</li><li>`failure` : avertit l’utilisateur ou l’utilisatrice en cas d’échec de la requête.</li><li>`quarantine` : s’active lorsqu’une exécution de requête planifiée est mise en quarantaine.</li></ul> La requête DELETE s’applique uniquement au type d’alerte spécifique fourni. |
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

Une réponse réussie renvoie un statut HTTP 200 et un message de confirmation incluant l’identifiant de la ressource et le type d’alerte de l’alerte supprimée.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Étapes suivantes

Ce guide couvre lʼutilisation du point d’entrée `/alert-subscriptions` dans lʼAPI Query Service. Après avoir lu ce guide, vous comprenez mieux comment créer une alerte pour une requête, abonner des utilisateurs à l’alerte, les types d’alertes disponibles et la manière dont les informations d’abonnement aux alertes peuvent être récupérées, mises à jour et supprimées.

Consultez le [guide de l’API Query Service](./getting-started.md) pour en savoir plus sur les autres fonctionnalités et opérations disponibles.
