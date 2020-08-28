---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation par flux
topic: developer guide
translation-type: tm+mt
source-git-commit: d35d598b2ae8b46f53a20d41770b21ceeeafcce8
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 40%

---


# Évaluer les événements en temps quasi réel avec la segmentation en flux continu

>[!NOTE]
>
>Le document suivant indique comment utiliser la segmentation en flux continu à l’aide de l’API. Pour plus d’informations sur l’utilisation de la segmentation en flux continu à l’aide de l’interface utilisateur, consultez le guide [de la segmentation en](../ui/streaming-segmentation.md)flux continu.

La segmentation en flux continu sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer la segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit maintenant lorsque les données en flux continu arrivent à destination [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. With this capability, most segment rules can now be evaluated as the data is passed into [!DNL Platform], meaning segment membership will be kept up-to-date without running scheduled segmentation jobs.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentation en flux continu ne peut être utilisée que pour évaluer les données diffusées en continu dans la plate-forme. En d’autres termes, les données ingérées par assimilation de lot ne seront pas évaluées par la segmentation en flux continu et nécessiteront le déclenchement de l’évaluation de lot.

## Prise en main

This developer guide requires a working understanding of the various [!DNL Adobe Experience Platform] services involved with streaming segmentation. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil unifié pour les consommateurs en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[ !Segmentation DNL]](../home.md): Permet de créer des segments et des audiences à partir de vos [!DNL Real-time Customer Profile] données.
- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Platform] APIs.

### Lecture d’exemples d’appels API

Ce guide de développement fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

Des en-têtes supplémentaires peuvent être nécessaires pour effectuer des requêtes spécifiques. Les en-têtes corrects sont présentés dans chacun des exemples de ce document. Accordez une attention particulière aux exemples de requêtes afin de vous assurer que tous les en-têtes requis sont inclus.

### Types de requête permettant la segmentation par flux {#streaming-segmentation-query-types}

>[!NOTE]
>
>Vous devez activer la segmentation planifiée pour l’organisation afin que la segmentation en flux continu fonctionne. Vous trouverez des informations sur l’activation de la segmentation planifiée dans la section [Activer la segmentation planifiée.](#enable-scheduled-segmentation)

Pour qu’un segment soit évalué à l’aide de la segmentation en flux continu, la requête doit se conformer aux directives suivantes.

| Type de requête | Détails |
| ---------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. |
| Accès entrant dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant **au cours des sept derniers jours**. |
| Profil uniquement | Toute définition de segment faisant référence uniquement à un attribut de profil. |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. |
| Accès entrant faisant référence à un profil dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant et à un ou plusieurs attributs de profil, **au cours des sept derniers jours**. |
| Plusieurs événements faisant référence à un profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. |

La section suivante liste des exemples de définition de segment qui **ne seront pas** activés pour la segmentation en flux continu.

| Type de requête | Détails |
| ---------- | ------- | 
| Accès entrant dans une fenêtre de temps relative | Si la définition de segment fait référence à un événement entrant **qui ne se trouve pas** dans la **dernière période** de sept jours. Par exemple, au cours des deux **dernières semaines**. |
| Accès entrant faisant référence à un profil dans une fenêtre relative | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>Événement entrant **non** compris dans la **dernière période** de sept jours.</li><li>Définition de segment qui comprend des segments ou des caractéristiques Adobe Audience Manager (AAM).</li></ul> |
| Plusieurs événements faisant référence à un profil | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>Événement qui **ne se produit pas** au cours **des dernières 24 heures**.</li><li>Définition de segment qui comprend des segments ou des caractéristiques Adobe Audience Manager (AAM).</li></ul> |
| Requêtes multientité | Les requêtes multientités **ne sont pas** prises en charge dans leur ensemble par la segmentation en flux continu. |

En outre, certaines directives s’appliquent lors de la segmentation en flux continu :

| Type de requête | Ligne directrice |
| ---------- | -------- |
| Requête événement unique | La fenêtre de rétrospective est limitée à **sept jours**. |
| Requête avec historique des événements | <ul><li>La fenêtre de rétrospective est limitée à **un jour**.</li><li>Une condition d’ordre temporel strict **doit** exister entre les événements.</li><li>Seules les commandes de temps simples (avant et après) entre les événements sont autorisées.</li><li>Les événements individuels **ne peuvent** être annulés. Cependant, toute la requête **peut** être annulée.</li></ul> |

## Récupérer tous les segments activés pour la segmentation en flux continu

Vous pouvez récupérer une liste de tous vos segments qui sont activés pour la segmentation en flux continu au sein de votre organisation IMS en adressant une demande de GET au point de `/segment/definitions` terminaison.

**Format d’API**

Pour récupérer les segments activés dans le flux, vous devez inclure le paramètre de requête `evaluationInfo.continuous.enabled=true` dans le chemin de requête.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de segments de votre organisation IMS permettant une segmentation par flux.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Création d’un segment activé dans le flux

Un segment est automatiquement activé en flux continu s’il correspond à l’un des types de segmentation de [flux continu répertoriés ci-dessus](#streaming-segmentation-query-types).

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>Il s’agit d’une requête standard &quot;créer un segment&quot;. For more information about creating a segment definition, please read the tutorial on [creating a segment](../tutorials/create-a-segment.md).

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle définition de segment activée dans le flux.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Activation de l’évaluation planifiée {#enable-scheduled-segmentation}

Une fois l’évaluation par flux activée, une ligne de base doit être créée (ensuite le segment sera toujours à jour). L’évaluation planifiée (également appelée segmentation planifiée) doit d’abord être activée pour que le système puisse exécuter automatiquement le nettoyage. Avec la segmentation planifiée, votre organisation IMS peut respecter un calendrier récurrent pour exécuter automatiquement des tâches d’exportation afin d’évaluer les segments.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. If your organization has more than five merge policies for [!DNL XDM Individual Profile] within a single sandbox environment, you will not be able to use scheduled evaluation.

### Création d’un planning

En effectuant une requête POST sur le point de terminaison `/config/schedules`, vous pouvez créer un planning et inclure l’heure spécifique à laquelle le planning doit être déclenché.

**Format d’API**

```http
POST /config/schedules
```

**Requête**

La requête suivante crée un planning en fonction des spécifications fournies dans le payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | **(Obligatoire)** Le nom du planning. Doit être une chaîne. |
| `type` | **(Obligatoire)** Le type de tâche au format chaîne. Les types `batch_segmentation` et `export` sont pris en charge. |
| `properties` | **(Obligatoire)** Un objet contenant des propriétés supplémentaires liées au planning. |
| `properties.segments` | **(Obligatoire lorsque`type`est égal à`batch_segmentation`)** L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `schedule` | **(Obligatoire)** Une chaîne contenant le planning de la tâche. Vous ne pouvez planifier qu’une seule exécution de tâche par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution d’une tâche plus d’une fois au cours d’une période de 24 heures. L’exemple illustré (`0 0 1 * * ?`) signifie que la tâche est déclenchée tous les jours à 1:00:00 UTC. Pour plus d’informations, consultez la documentation sur le [format d’expression cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). |
| `state` | *(Facultatif)* Chaîne contenant l’état du planning. Valeurs disponibles : `active` et `inactive`. La valeur par défaut est `inactive`. Une organisation IMS ne peut créer qu’un seul planning. Les étapes de mise à jour du planning sont disponibles plus loin dans ce tutoriel. |

**Réponse**

Une réponse réussie renvoie les détails du planning créé.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Activation d’un planning

Par défaut, un planning est inactif lors de la création, sauf si la propriété `state` est définie sur `active` dans le corps de la requête de création (POST). Vous pouvez activer un planning (définissez `state` sur `active`) en effectuant une requête PATCH sur le point de terminaison `/config/schedules` et en incluant l’identifiant du planning dans le chemin.

**Format d’API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Requête**

La requête suivante utilise le [format du correctif JSON](http://jsonpatch.com/) pour mettre à jour l’état `state` du planning sur `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Réponse**

Une mise à jour réussie renvoie un corps de réponse vide et un état HTTP 204 (No Content).

La même opération peut être utilisée pour désactiver un planning en remplaçant la « valeur » de la requête précédente par « inactif ».

## Étapes suivantes

Maintenant que vous avez activé la segmentation par flux pour les nouveaux segments et les segments existants, et que vous avez activé la segmentation planifiée pour développer une ligne de base et effectuer des évaluations récurrentes, vous pouvez commencer à créer des segments pour votre organisation.

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le [guide d’utilisation du créateur de segments](../ui/segment-builder.md).