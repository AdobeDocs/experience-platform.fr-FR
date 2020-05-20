---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Planifications
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 4%

---


# Guide du développeur de calendriers

intro

- Récupérer une liste de planification
- Créer une planification
- Récupérer un calendrier spécifique
- Mettre à jour un calendrier spécifique
- Supprimer un calendrier spécifique

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API de segmentation. Avant de continuer, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [Prise en main de la](./getting-started.md#getting-started) sectiondu guide du développeur de segmentation contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Récupérer une liste de planification

Vous pouvez récupérer une liste de toutes les planifications pour votre organisation IMS en adressant une demande GET au point de `/config/schedules` terminaison.

**Format d’API**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres de Requête**

Vous trouverez ci-dessous une liste des paramètres de requête disponibles pour les planifications de mise en vente. Tous ces paramètres sont facultatifs. Effectuer un appel vers ce point de terminaison sans paramètres récupérera toutes les planifications disponibles pour votre organisation.

| Paramètre | Description |
| --------- | ----------- |
| `start` | Indique la page à partir de laquelle le décalage sera début. Par défaut, cette valeur sera 0. |
| `limit` | Indique le nombre de planifications renvoyées. Par défaut, cette valeur sera de 100. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste de planification pour l’organisation IMS spécifiée en tant que JSON.

```json
{
    "_page": {
        "totalCount": 1,
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

## Créer une planification

Vous pouvez créer une planification en adressant une requête POST au point de `/config/schedules` terminaison.

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
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| Paramètre | Description |
| --------- | ------------ |
| `name` | **Obligatoire.** Nom de la planification sous forme de chaîne. |
| `type` | **Obligatoire.** Type de la tâche sous forme de chaîne. Les deux types pris en charge sont `batch_segmentation` et `export`. |
| `properties` | **Obligatoire.** Objet contenant des propriétés supplémentaires liées à la planification. |
| `properties.segments` | **Obligatoire lorsque`type`est égal`batch_segmentation`.** L’utilisation `["*"]` de cette option garantit l’inclusion de tous les segments. |
| `schedule` | **Obligatoire.** Chaîne contenant la planification de la tâche. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [d&#39;expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. Dans cet exemple, &quot;0 0 1 *&quot; signifie que cette planification s’exécutera à minuit le premier de chaque mois. |
| `state` | *Facultatif.* Chaîne contenant l&#39;état de planification. Les deux États soutenus sont `active` et `inactive`. By default, the state is set to `inactive`. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de votre planification nouvellement créée.

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

## Récupérer un calendrier spécifique

Vous pouvez récupérer des informations détaillées sur une planification spécifique en envoyant une requête GET au point de `/config/schedules` terminaison et en indiquant la `id` valeur de la planification dans le chemin de requête.

**Format d’API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Valeur `id` de la planification que vous souhaitez récupérer.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur la planification spécifiée.

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
```

## Mettre à jour détaille un calendrier spécifique

Vous pouvez mettre à jour une planification spécifiée en exécutant une requête PATCH sur le point de `/config/schedules` terminaison et en indiquant la `id` valeur de la planification dans le chemin de requête.

La demande PATCH prend en charge deux chemins différents : `/state` et `/schedule`.

### Mettre à jour l&#39;état de planification

Vous pouvez utiliser `/state` pour mettre à jour l’état de la planification : ACTIVE ou INACTIVE. Pour mettre à jour l’état, vous devez définir la valeur comme `active` ou `inactive`.

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Valeur `id` de la planification que vous souhaitez mettre à jour.

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
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
]
'
```

| Paramètre | Description |
| --------- | ----------- |
| `path` | Chemin d’accès de la valeur à appliquer. Dans ce cas, puisque vous mettez à jour l&#39;état de la planification, vous devez définir la valeur de `path` sur `/state`. |
| `value` | Valeur mise à jour de la `/state`. Cette valeur peut être définie comme `active` ou `inactive` pour activer ou désactiver la planification. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (aucun contenu).

### Mettre à jour la planification cron

Vous pouvez utiliser `schedule` pour mettre à jour la planification cron. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [d&#39;expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron.

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Valeur `id` de la planification que vous souhaitez mettre à jour.

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| Paramètre | Description |
| --------- | ----------- |
| `path` | Chemin d’accès de la valeur à appliquer. Dans ce cas, puisque vous mettez à jour la planification cron de la planification, vous devez définir la valeur de `path` sur `/schedule`. |
| `value` | Valeur mise à jour de la `/state`. Cette valeur doit prendre la forme d’un calendrier cron. Dans cet exemple, la planification s’exécutera le deuxième de chaque mois. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (aucun contenu).

## Supprimer un calendrier spécifique

Vous pouvez demander la suppression d&#39;un calendrier spécifié en adressant une requête DELETE à l&#39;utilisateur `/config/schedules` et en indiquant la `id` valeur du calendrier dans le chemin de la demande.

**Format d’API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: Valeur `id` de la planification à supprimer.

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (Aucun contenu) avec le message suivant :

```json
(No Content) Schedule deleted successfully
```

## Étapes suivantes
