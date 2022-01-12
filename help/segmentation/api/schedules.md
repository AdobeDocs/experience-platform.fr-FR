---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;plannings;planification;api;API;
solution: Experience Platform
title: Point de terminaison de l’API Schedules
topic-legacy: developer guide
description: Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des tâches de segmentation par lots une fois par jour.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 46%

---

# Point de terminaison des planifications

Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser la variable `/config/schedules` point de fin pour récupérer une liste de plannings, créer un nouveau planning, récupérer les détails d’un planning spécifique, mettre à jour un planning spécifique ou supprimer un planning spécifique.

## Prise en main

Les points d’entrée d’API utilisés dans ce guide font partie de l’[!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels à l’API, notamment les en-têtes requis et la lecture d’exemples d’appels API.

## Obtention d’une liste de plannings {#retrieve-list}

Vous pouvez obtenir une liste de tous les plannings de votre organisation IMS en faisant une requête GET au point de terminaison `/config/schedules`.

**Format d’API**

Le point d’entrée `/config/schedules` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés. En passant un appel vers ce point de terminaison sans paramètres, vous récupérerez tous les plannings disponibles pour votre organisation. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

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

La requête suivante récupérera les dix derniers plannings publiés dans votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de plannings pour l’organisation IMS spécifiée en tant que JSON.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace et affiche uniquement la première planification renvoyée.

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
| `_page.totalCount` | Nombre total de plannings renvoyés. |
| `_page.pageSize` | Taille de la page des plannings. |
| `children.name` | Nom du planning sous forme de chaîne. |
| `children.type` | Type de tâche sous forme de chaîne. Les deux types pris en charge sont &quot;batch_segmentation&quot; et &quot;export&quot;. |
| `children.properties` | Objet contenant des propriétés supplémentaires liées au planning. |
| `children.properties.segments` | L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `children.schedule` | Chaîne contenant le planning de la tâche. L’exécution des tâches ne peut être planifiée qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution de plusieurs tâches sur une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 0 0 1 * * » signifie que ce planning sera exécuté à minuit le premier de chaque mois. |
| `children.state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont &quot;principal&quot; et &quot;inactif&quot;. Par défaut, l’état est défini sur &quot;inactif&quot;. |

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
| `properties.segments` | **Obligatoire lorsque `type` est égal à &quot;batch_segmentation&quot;.** L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `schedule` | *Facultatif.* Chaîne contenant le planning de la tâche. L’exécution des tâches ne peut être planifiée qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution de plusieurs tâches sur une période de 24 heures. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 0 0 1 * * » signifie que ce planning sera exécuté à minuit le premier de chaque mois. <br><br>Si cette chaîne n’est pas fournie, un planning généré automatiquement. |
| `state` | *Facultatif.* Chaîne contenant l’état du planning. Les deux états pris en charge sont &quot;principal&quot; et &quot;inactif&quot;. Par défaut, l’état est défini sur &quot;inactif&quot;. |

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

Vous pouvez récupérer des informations détaillées sur un planning spécifique en envoyant une requête de GET au `/config/schedules` point de terminaison et en indiquant l’identifiant du planning que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur du planning que vous souhaitez récupérer. |

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
| `schedule` | Chaîne contenant le planning de la tâche. Vous ne pouvez planifier qu’une seule exécution de tâche par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution d’une tâche plus d’une fois au cours d’une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). Dans cet exemple, « 0 0 1 * * » signifie que ce planning sera exécuté à minuit le premier de chaque mois. |
| `state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont `active` et `inactive`. Par défaut, l’état est défini sur `inactive`. |

## Mise à jour des détails d’un planning spécifique {#update}

Vous pouvez mettre à jour un planning spécifique en envoyant une requête de PATCH au `/config/schedules` point de terminaison et en indiquant l’identifiant du planning que vous essayez de mettre à jour dans le chemin de requête.

La requête du PATCH vous permet de mettre à jour la variable [state](#update-state) ou le [planning cron](#update-schedule) pour un planning individuel.

### Mise à jour de l’état du planning {#update-state}

Vous pouvez utiliser une opération de correctif JSON pour mettre à jour l’état du planning. Pour mettre à jour l’état, vous déclarez la variable `path` property as `/state` et définissez la variable `value` à `active` ou `inactive`. Pour plus d’informations sur le correctif JSON, veuillez lire la section [Correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentation.

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur du planning que vous souhaitez mettre à jour. |

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
| `path` | Chemin d’accès de la valeur que vous souhaitez mettre à jour. Dans ce cas, puisque vous mettez à jour l’état du planning, vous devez définir la valeur de `path` à &quot;/state&quot;. |
| `value` | Valeur mise à jour de l’état du planning. Cette valeur peut être définie sur &quot;principal&quot; ou &quot;inactif&quot; pour activer ou désactiver le planning. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

### Mise à jour du planning cron {#update-schedule}

Vous pouvez utiliser une opération de correctif JSON pour mettre à jour le planning cron. Pour mettre à jour le planning, vous devez déclarer la variable `path` property as `/schedule` et définissez la variable `value` à un planning cron valide. Pour plus d’informations sur le correctif JSON, veuillez lire la section [Correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentation. Pour plus d’informations sur les plannings cron, consultez la documentation sur le [format d’expression cron](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur du planning que vous souhaitez mettre à jour. |

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
| `path` | Chemin d’accès de la valeur que vous souhaitez mettre à jour. Dans ce cas, puisque vous mettez à jour le planning cron, vous devez définir la valeur de `path` to `/schedule`. |
| `value` | La valeur mise à jour du planning cron. Cette valeur doit se présenter sous la forme d’un planning cron. Dans cet exemple, le planning se déroulera le deuxième jour de chaque mois. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

## Suppression d’un planning spécifique

Vous pouvez demander la suppression d’un planning spécifique en adressant une requête de DELETE au `/config/schedules` et en indiquant l’identifiant du planning que vous souhaitez supprimer dans le chemin d’accès à la requête.

**Format d’API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Le `id` valeur du planning que vous souhaitez supprimer. |

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

Après avoir lu ce guide, vous comprenez mieux le fonctionnement des plannings.
