---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Plannings
topic: developer guide
translation-type: tm+mt
source-git-commit: 842f31aac2bdbf7e9f79e4ae7d4c36be1dc92392
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 47%

---


# Guide du point de terminaison des calendriers

Les calendriers sont un outil qui permet d&#39;exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser le `/config/schedules` point de terminaison pour récupérer une liste de planifications, créer une nouvelle planification, récupérer les détails d&#39;une planification spécifique, mettre à jour une planification spécifique ou supprimer une planification spécifique.

## Prise en main

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Obtention d’une liste de plannings {#retrieve-list}

Vous pouvez obtenir une liste de tous les plannings de votre organisation IMS en faisant une requête GET au point de terminaison `/config/schedules`.

**Format d’API**

Le `/config/schedules` point de terminaison prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est fortement recommandée pour réduire les frais généraux élevés. En passant un appel vers ce point de terminaison sans paramètres, vous récupérerez tous les plannings disponibles pour votre organisation. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Paramètre | Description |
| --------- | ----------- |
| `{START}` | Spécifie la page à partir de laquelle le décalage commencera. Par défaut, cette valeur sera définie sur 0. |
| `{LIMIT}` | Indique le nombre de plannings renvoyés. Par défaut, cette valeur sera définie sur 100. |

**Requête**

La demande suivante récupérera les dix dernières annexes publiées dans votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de plannings pour l’organisation IMS spécifiée en tant que JSON.

>[!NOTE] La réponse suivante a été tronquée pour l’espace et affiche uniquement la première planification renvoyée.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propriété | Description |
| -------- | ------------ |
| `_page.totalCount` | Nombre total de planifications renvoyées. |
| `_page.pageSize` | Taille de la page des planifications. |
| `children.name` | Nom du planning sous forme de chaîne. |
| `children.type` | Type de tâche sous forme de chaîne. Les deux types pris en charge sont &quot;batch_segmentation&quot; et &quot;export&quot;. |
| `children.properties` | Objet contenant des propriétés supplémentaires liées au planning. |
| `children.properties.segments` | L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `children.schedule` | Chaîne contenant le planning de la tâche. Les tâches ne peuvent être planifiées qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier une tâche pour qu’elle s’exécute plusieurs fois au cours d’une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire la documentation sur le [format d’expression cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 0 0 1 * * » signifie que ce planning sera exécuté à minuit le premier de chaque mois. |
| `children.state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont &quot;actifs&quot; et &quot;inactifs&quot;. Par défaut, l’état est défini sur &quot;inactif&quot;. |

## Création d’un nouveau planning {#create}

Vous pouvez créer un nouveau planning en effectuant une requête POST au point de terminaison `/config/schedules`.

**Format d’API**

```http
POST /config/schedules
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Propriété | Description |
| -------- | ------------ |
| `name` | **Obligatoire.** Nom du planning sous forme de chaîne. |
| `type` | **Obligatoire.** Type de tâche sous forme de chaîne. Les deux types pris en charge sont &quot;batch_segmentation&quot; et &quot;export&quot;. |
| `properties` | **Obligatoire.** Objet contenant des propriétés supplémentaires liées au planning. |
| `properties.segments` | **Obligatoire lorsque`type`est égal à &quot;batch_segmentation&quot;.** L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `schedule` | *Facultatif.* Chaîne contenant le planning de la tâche. Les tâches ne peuvent être planifiées qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier une tâche pour qu’elle s’exécute plusieurs fois au cours d’une période de 24 heures. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 0 0 1 * * » signifie que ce planning sera exécuté à minuit le premier de chaque mois. <br><br>Si cette chaîne n&#39;est pas fournie, un calendrier généré par le système est généré automatiquement. |
| `state` | *Facultatif.* Chaîne contenant l’état du planning. Les deux états pris en charge sont &quot;actifs&quot; et &quot;inactifs&quot;. Par défaut, l’état est défini sur &quot;inactif&quot;. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de votre nouveau planning.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
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

## Récupération d’un planning spécifique {#get}

You can retrieve detailed information about a specific schedule by making a GET request to the `/config/schedules` endpoint and providing the ID of the schedule you wish to retrieve in the request path.

**Format d’API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the schedule you want to retrieve. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur le planning spécifié.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
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

| Propriété | Description |
| -------- | ------------ |
| `name` | Nom du planning sous forme de chaîne. |
| `type` | Type de tâche sous forme de chaîne. Les deux types pris en charge sont `batch_segmentation` et `export`. |
| `properties` | Objet contenant des propriétés supplémentaires liées au planning. |
| `properties.segments` | L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `schedule` | Chaîne contenant le planning de la tâche. Vous ne pouvez planifier qu’une seule exécution de tâche par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution d’une tâche plus d’une fois au cours d’une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire la documentation sur le [format d’expression cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 0 0 1 * * » signifie que ce planning sera exécuté à minuit le premier de chaque mois. |
| `state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont `active` et `inactive`. Par défaut, l’état est défini sur `inactive`. |

## Update details for a specific schedule {#update}

Vous pouvez mettre à jour une planification spécifique en exécutant une requête PATCH sur le point de `/config/schedules` terminaison et en indiquant l&#39;ID de la planification que vous tentez de mettre à jour dans le chemin de la requête.

La demande PATCH vous permet de mettre à jour l&#39; [état](#update-state) ou le calendrier [](#update-schedule) cron pour un calendrier individuel.

### Mise à jour de l’état du planning {#update-state}

Vous pouvez utiliser une opération de correctif JSON pour mettre à jour l’état de la planification. Pour mettre à jour l’état, vous déclarez la `path` propriété comme `/state` et définissez la `value` propriété sur `active` ou `inactive`. Pour plus d’informations sur le correctif JSON, consultez la documentation sur le correctif [](http://jsonpatch.com/) JSON.

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the schedule you want to update. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op": "add",
        "path": "/state",
        "value": "active"
    }
]'
```

| Propriété | Description |
| -------- | ----------- |
| `path` | Chemin d’accès de la valeur que vous souhaitez mettre à jour. In this case, since you are updating the schedule&#39;s state, you need to set the value of `path` to &quot;/state&quot;. |
| `value` | Valeur mise à jour de l&#39;état de la planification. Cette valeur peut être définie comme &quot;active&quot; ou &quot;inactive&quot; pour activer ou désactiver la planification. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

### Mise à jour du calendrier cron {#update-schedule}

Vous pouvez utiliser une opération de correctif JSON pour mettre à jour la planification cron. Pour mettre à jour la planification, vous déclarez la `path` propriété comme `/schedule` et définissez la `value` propriété sur une planification cron valide. Pour plus d’informations sur le correctif JSON, consultez la documentation sur le correctif [](http://jsonpatch.com/) JSON. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the schedule you want to update. |

**Requête**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Propriété | Description |
| -------- | ----------- |
| `path` | Chemin d’accès de la valeur à mettre à jour. In this case, since you are updating the cron schedule, you need to set the value of `path` to `/schedule`. |
| `value` | Valeur mise à jour de la planification cron. Cette valeur doit se présenter sous la forme d’un planning cron. Dans cet exemple, le planning se déroulera le deuxième jour de chaque mois. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

## Suppression d’un planning spécifique

You can request to delete a specific schedule by making a DELETE request to the `/config/schedules` endpoint and providing the ID of the schedule you wish to delete in the request path.

**Format d’API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | The `id` value of the schedule you want to delete. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment fonctionnent les horaires.