---
solution: Experience Platform
title: Point de terminaison de l’API Schedules
description: Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des tâches de segmentation par lots une fois par jour.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 16%

---

# Point de terminaison des planifications

Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des tâches de segmentation par lots une fois par jour. Vous pouvez utiliser la variable `/config/schedules` point de fin pour récupérer une liste de plannings, créer un nouveau planning, récupérer les détails d’un planning spécifique, mettre à jour un planning spécifique ou supprimer un planning spécifique.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de la variable [!DNL Adobe Experience Platform Segmentation Service] API. Avant de poursuivre, veuillez consulter la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels à l’API, notamment les en-têtes requis et la lecture d’exemples d’appels API.

## Obtention d’une liste de plannings {#retrieve-list}

Vous pouvez récupérer une liste de tous les plannings de votre organisation en envoyant une requête de GET au `/config/schedules` point de terminaison .

**Format d’API**

Le point d’entrée `/config/schedules` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés. Un appel à ce point de terminaison sans paramètres permet de récupérer toutes les plannings disponibles pour votre organisation. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

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

La requête suivante récupère les dix derniers plannings publiés au sein de votre organisation.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste de plannings pour l’organisation spécifiée comme JSON.

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
            "imsOrgId": "{ORG_ID}",
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
| `children.properties.segments` | Utilisation `["*"]` s’assure que tous les segments sont inclus. |
| `children.schedule` | Chaîne contenant le planning de la tâche. L’exécution des tâches ne peut être planifiée qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution de plusieurs tâches sur une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire l’annexe sur la page [format d’expression cron](#appendix). Dans cet exemple, &quot;0 0 1 * *&quot; signifie que cette planification s’exécutera à 1h00 tous les jours. |
| `children.state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont &quot;actif&quot; et &quot;inactif&quot;. Par défaut, l’état est défini sur &quot;inactif&quot;. |

## Création d’un nouveau planning {#create}

Vous pouvez créer un nouveau planning en effectuant une requête POST au point d’entrée `/config/schedules`.

**Format d’API**

```http
POST /config/schedules
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schedule` | *Facultatif.* Chaîne contenant le planning de la tâche. L’exécution des tâches ne peut être planifiée qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution de plusieurs tâches sur une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire l’annexe sur la page [format d’expression cron](#appendix). Dans cet exemple, &quot;0 0 1 * *&quot; signifie que cette planification s’exécutera à 1h00 tous les jours. <br><br>Si cette chaîne n’est pas fournie, un planning généré automatiquement. |
| `state` | *Facultatif.* Chaîne contenant l’état du planning. Les deux états pris en charge sont &quot;actif&quot; et &quot;inactif&quot;. Par défaut, l’état est défini sur &quot;inactif&quot;. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de votre nouveau planning.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `{SCHEDULE_ID}` | La variable `id` valeur du planning que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur le planning spécifié.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `properties.segments` | Utilisation `["*"]` s’assure que tous les segments sont inclus. |
| `schedule` | Chaîne contenant le planning de la tâche. Vous ne pouvez planifier qu’une seule exécution de tâche par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution d’une tâche plus d’une fois au cours d’une période de 24 heures. Pour plus d’informations sur les plannings cron, veuillez lire l’annexe sur la page [format d’expression cron](#appendix). Dans cet exemple, &quot;0 0 1 * *&quot; signifie que cette planification s’exécutera à 1h00 tous les jours. |
| `state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont `active` et `inactive`. Par défaut, l’état est défini sur `inactive`. |

## Mise à jour des détails d’un planning spécifique {#update}

Vous pouvez mettre à jour un planning spécifique en envoyant une requête de PATCH au `/config/schedules` point de terminaison et en indiquant l’identifiant du planning que vous essayez de mettre à jour dans le chemin d’accès de la requête.

La requête du PATCH vous permet de mettre à jour la variable [state](#update-state) ou le [planning cron](#update-schedule) pour un planning individuel.

### Mise à jour de l’état du planning {#update-state}

Vous pouvez utiliser une opération de correctif JSON pour mettre à jour l’état du planning. Pour mettre à jour l’état, vous déclarez la variable `path` property as `/state` et définissez la variable `value` à `active` ou `inactive`. Pour plus d’informations sur le correctif JSON, veuillez lire la section [Correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902) la documentation.

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` valeur du planning que vous souhaitez mettre à jour. |

**Requête**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `value` | Valeur mise à jour de l’état du planning. Cette valeur peut être définie sur &quot;actif&quot; ou &quot;inactif&quot; pour activer ou désactiver le planning. Veuillez noter que vous **cannot** désactivez une planification si l’organisation a été activée pour la diffusion en continu. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

### Mise à jour du planning cron {#update-schedule}

Vous pouvez utiliser une opération de correctif JSON pour mettre à jour le planning cron. Pour mettre à jour le planning, vous devez déclarer la variable `path` property as `/schedule` et définissez la variable `value` à un planning cron valide. Pour plus d’informations sur le correctif JSON, veuillez lire la section [Correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902) la documentation. Pour plus d’informations sur les plannings cron, veuillez lire l’annexe sur la page [format d’expression cron](#appendix).

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | La variable `id` valeur du planning que vous souhaitez mettre à jour. |

**Requête**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
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
| `{SCHEDULE_ID}` | La variable `id` valeur du planning que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux le fonctionnement des plannings.

## Annexe {#appendix}

L’annexe suivante explique le format des expressions cron utilisées dans les plannings.

### Format

Une expression cron est une chaîne composée de 6 ou 7 champs. L’expression ressemble à ce qui suit :

`0 0 12 * * ?`

Dans une chaîne d’expression cron, le premier champ représente les secondes, le second les minutes, le troisième les heures, le quatrième le jour du mois, le cinquième le mois et le sixième le jour de la semaine. Vous pouvez également inclure un septième champ, qui représente l’année.

| Nom du champ | Obligatoire | Valeurs possibles | Caractères spéciaux autorisés |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Oui | 0 à 59 | `, - * /` |
| Minutes | Oui | 0 à 59 | `, - * /` |
| Heures | Oui | 0-23 | `, - * /` |
| Jour du mois | Oui | 1-31 | `, - * ? / L W` |
| Mois | Oui | 1-12, JAN-DEC | `, - * /` |
| Jour de la semaine | Oui | 1-7, SUN-SAT | `, - * ? / L #` |
| Année | Non | Vide, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Les noms des mois et des jours de la semaine sont **not** sensible à la casse. Par conséquent, `SUN` équivaut à utiliser `sun`.

Les caractères spéciaux autorisés représentent les significations suivantes :

| Caractère spécial | Description |
| ----------------- | ----------- |
| `*` | Cette valeur est utilisée pour sélectionner **all** dans un champ. Par exemple, la méthode `*` dans le champ heures signifierait **each** heure. |
| `?` | Cette valeur signifie qu’aucune valeur spécifique n’est requise. Cette option est généralement utilisée pour spécifier quelque chose dans un champ où le caractère est autorisé, mais pas dans l’autre champ. Par exemple, si vous souhaitez qu’un événement se déclenche tous les 3 du mois, mais que vous ne vous souciez pas du jour de la semaine, vous pouvez définir `3` dans le champ jour du mois et `?` dans le champ jour de la semaine. |
| `-` | Cette valeur est utilisée pour spécifier **inclusif** plages pour le champ . Par exemple, si vous placez `9-15` dans le champ heures , cela signifie que les heures comprennent 9, 10, 11, 12, 13, 14 et 15. |
| `,` | Cette valeur est utilisée pour spécifier des valeurs supplémentaires. Par exemple, si vous placez `MON, FRI, SAT` dans le champ jour de la semaine , cela signifie que les jours de la semaine comprennent le lundi, le vendredi et le samedi. |
| `/` | Cette valeur est utilisée pour spécifier des incréments. La valeur placée avant la variable `/` détermine d’où il est incrémenté, tandis que la valeur placée après la propriété `/` détermine la valeur de son incrément. Par exemple, si vous placez `1/7` dans le champ minutes , cela signifie que les minutes comprennent 1, 8, 15, 22, 29, 36, 43, 50 et 57. |
| `L` | Cette valeur est utilisée pour spécifier `Last`, et a une signification différente selon le champ dans lequel elle est utilisée. S’il est utilisé avec le champ jour du mois, il représente le dernier jour du mois. S’il est utilisé seul avec le champ Jour de la semaine, il représente le dernier jour de la semaine, qui est samedi (`SAT`). S’il est utilisé avec le champ Jour de la semaine, conjointement avec une autre valeur, il représente le dernier jour de ce type pour le mois. Par exemple, si vous placez `5L` dans le champ jour de la semaine, il **only** inclut le dernier vendredi du mois. |
| `W` | Cette valeur est utilisée pour spécifier le jour de la semaine le plus proche du jour donné. Par exemple, si vous placez `18W` dans le champ jour du mois, et le 18 de ce mois était un samedi, il se déclenchait le vendredi 17, qui est le jour de semaine le plus proche. Si le 18 de ce mois était un dimanche, il se déclencherait le lundi 19, qui est le jour de semaine le plus proche. Veuillez noter que si vous placez `1W` dans le champ jour du mois , et que le jour de semaine le plus proche se situe dans le mois précédent, l’événement se déclenche toujours le jour de semaine le plus proche de la variable **current** le mois.</br></br>De plus, vous pouvez combiner des `L` et `W` pour créer `LW`, qui spécifie le dernier jour de semaine du mois. |
| `#` | Cette valeur est utilisée pour spécifier le énième jour de la semaine d’un mois. La valeur placée avant la variable `#` représente le jour de la semaine, tandis que la valeur placée après la variable `#` représente l’occurrence du mois. Par exemple, si vous placez `1#3`, l’événement se déclenche le troisième dimanche du mois. Veuillez noter que si vous placez `X#5` et il n’y a pas de cinquième occurrence de ce jour de la semaine ce mois-ci, l’événement **not** être déclenchée. Par exemple, si vous placez `1#5`, et il n’y a pas de cinquième dimanche dans ce mois-ci, l’événement aura lieu le 24 novembre 2010. **not** être déclenchée. |

### Exemples

Le tableau suivant présente des exemples de chaînes d’expression cron et explique leur signification.

| Expression | Explication |
| ---------- | ----------- |
| `0 0 13 * * ?` | L&#39;événement se déclenchera tous les jours à 13h00. |
| `0 30 9 * * ? 2022` | L&#39;événement se déclenchera tous les jours à 9h30 en 2022. |
| `0 * 18 * * ?` | L&#39;événement se déclenche toutes les minutes, de 18h à 18h59, tous les jours. |
| `0 0/10 17 * * ?` | L&#39;événement se déclenche toutes les 10 minutes, de 17h à 18h, chaque jour. |
| `0 13,38 5 ? 6 WED` | L&#39;événement se déclenchera à 5h13 et 5h38 tous les mercredis du mois de juin. |
| `0 30 12 ? * 4#3` | L&#39;événement se déclenchera à 12h30 le troisième mercredi tous les mois. |
| `0 30 12 ? * 6L` | L’événement se déclenchera à 12h30 le dernier vendredi de chaque mois. |
| `0 45 11 ? * MON-THU` | L’événement se déclenchera à 11h45 tous les lundis, mardis, mercredis et jeudis. |