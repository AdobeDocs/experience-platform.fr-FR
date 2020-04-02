---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Planifications
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Guide du développeur de calendriers

intro

- Récupération d’un  de planification
- Créer une planification
- Récupérer un calendrier spécifique
- Mettre à jour un calendrier spécifique
- Suppression d’un calendrier spécifique

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de segmentation. Avant de poursuivre, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [de](./getting-started.md#getting-started) prise en main du guide du développeur de segmentation comprend des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le  du et des informations importantes concernant les en-têtes requis nécessaires pour effectuer des appels à une API de plateforme d’expérience.

## Récupération d’un  de planification

Vous pouvez récupérer un de tous les planifications pour votre organisation IMS en faisant une demande GET au point de `/config/schedules` terminaison.

**Format API**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres**

Vous trouverez ci-dessous un  des paramètres de disponibles pour les planifications de liste. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètres récupérera toutes les planifications disponibles pour votre entreprise.

| Paramètre | Description |
| --------- | ----------- |
| `start` | Indique de quelle page le décalage . Par défaut, cette valeur sera 0. |
| `limit` | Indique le nombre de planifications renvoyées. Par défaut, cette valeur sera 100. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un de planifications pour l’organisation IMS spécifiée en tant que JSON.

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

Vous pouvez créer une planification en faisant une requête POST au point de `/config/schedules` fin.

**Format API**

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
| `type` | **Obligatoire.** Type de tâche sous forme de chaîne. Les deux types pris en charge sont `batch_segmentation` et `export`. |
| `properties` | **Obligatoire.** Objet contenant des propriétés supplémentaires liées à la planification. |
| `properties.segments` | **Obligatoire lorsque`type`est égal`batch_segmentation`.** L’utilisation de `["*"]` cette option permet de s’assurer que tous les segments sont inclus. |
| `schedule` | **Obligatoire.** Chaîne contenant la planification de la tâche. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [de ](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron . Dans cet exemple, &quot;0 0 1 *&quot; signifie que cette planification s’exécutera à minuit le premier de chaque mois. |
| `state` | *Facultatif.* Chaîne contenant l’état de planification. Les deux états pris en charge sont `active` et `inactive`. By default, the state is set to `inactive`. |

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

Vous pouvez récupérer des informations détaillées sur un calendrier spécifique en envoyant une requête GET au point de `/config/schedules` fin et en indiquant la `id` valeur du calendrier dans le chemin de requête.

**Format API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: La `id` valeur de la planification que vous souhaitez récupérer.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur le calendrier spécifié.

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

Vous pouvez mettre à jour une planification spécifiée en effectuant une requête PATCH sur le `/config/schedules` point de fin et en indiquant la `id` valeur de la planification dans le chemin de la requête.

La requête PATCH prend en charge deux chemins différents : `/state` et `/schedule`.

### Mettre à jour l&#39;état de planification

Vous pouvez utiliser `/state` pour mettre à jour l’état de la planification - ACTIF ou INACTIF. Pour mettre à jour l’état, vous devez définir la valeur sur `active` ou `inactive`.

**Format API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: La `id` valeur de la planification que vous souhaitez mettre à jour.

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
| `path` | Chemin d’accès de la valeur que vous souhaitez appliquer au correctif. Dans ce cas, puisque vous mettez à jour l’état de la planification, vous devez définir la valeur de `path` sur `/state`. |
| `value` | Valeur mise à jour de la `/state`. Cette valeur peut être définie sur `active` ou `inactive` pour activer ou désactiver la planification. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (aucun contenu).

### Mettre à jour le calendrier cron

Vous pouvez utiliser `schedule` pour mettre à jour la planification de cron. Pour plus d&#39;informations sur les calendriers cron, veuillez lire la documentation sur le format [de ](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron .

**Format API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`: La `id` valeur de la planification que vous souhaitez mettre à jour.

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
| `path` | Chemin d’accès de la valeur que vous souhaitez appliquer au correctif. Dans ce cas, puisque vous mettez à jour la planification cron, vous devez définir la valeur de `path` sur `/schedule`. |
| `value` | Valeur mise à jour de la `/state`. Cette valeur doit prendre la forme d’un calendrier cron. Dans cet exemple, la planification s’exécutera le deuxième de chaque mois. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (aucun contenu).

## Suppression d’un calendrier spécifique

Vous pouvez demander de supprimer une planification spécifiée en faisant une requête DELETE à la `/config/schedules` et en indiquant la `id` valeur de la planification dans le chemin de la demande.

**Format API**

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

Une réponse réussie renvoie l’état HTTP 204 (aucun contenu) avec le message suivant :

```json
(No Content) Schedule deleted successfully
```

## Étapes suivantes
