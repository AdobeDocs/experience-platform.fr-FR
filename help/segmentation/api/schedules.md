---
solution: Experience Platform
title: Point d’entrée de l’API Schedules
description: Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des traitements de segmentation par lots une fois par jour.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 15%

---

# Point d’entrée des plannings

Les planifications sont un outil qui peut être utilisé pour exécuter automatiquement des traitements de segmentation par lots une fois par jour. Vous pouvez utiliser le point d’entrée `/config/schedules` pour récupérer une liste de planifications, créer une nouvelle planification, récupérer les détails d’une planification spécifique, mettre à jour une planification spécifique ou supprimer une planification spécifique.

## Commencer

Les points d’entrée utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

## Obtention d’une liste de plannings {#retrieve-list}

Vous pouvez récupérer une liste de tous les plannings pour votre organisation en envoyant une requête GET au point d’entrée `/config/schedules`.

**Format d’API**

Le point d’entrée `/config/schedules` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés. Si vous effectuez un appel à ce point d’entrée sans paramètre, toutes les planifications disponibles pour votre organisation sont récupérées. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**Paramètres de requête**

+++ Liste des paramètres de requête disponibles.

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `start` | Spécifie la page à partir de laquelle le décalage commencera. Par défaut, cette valeur sera définie sur 0. | `start=5` |
| `limit` | Indique le nombre de plannings renvoyés. Par défaut, cette valeur sera définie sur 100. | `limit=20` |

+++

**Requête**

La requête suivante récupère les dix dernières planifications publiées au sein de votre organisation.

+++ Exemple de requête pour récupérer une liste de plannings.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec une liste de plannings pour l’organisation spécifiée au format JSON.

>[!NOTE]
>
>La réponse suivante a été tronquée pour des raisons d’espace et n’affiche que le premier planning renvoyé.

+++ Exemple de réponse lors de la récupération d’une liste de plannings.

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
| `children.type` | Type de traitement sous forme de chaîne. Les deux types pris en charge sont « batch_segmentation » et « export ». |
| `children.properties` | Objet contenant des propriétés supplémentaires liées au planning. |
| `children.properties.segments` | L’utilisation de `["*"]` garantit que tous les segments sont inclus. |
| `children.schedule` | Chaîne contenant le planning du traitement. Les tâches ne peuvent être planifiées pour s’exécuter qu’une seule fois par jour, ce qui signifie que vous ne pouvez pas planifier une tâche pour qu’elle s’exécute plus d’une fois sur une période de 24 heures. Pour plus d’informations sur les plannings cron, consultez l’annexe sur le [format d’expression cron](#appendix). Dans cet exemple, « `0 0 1 * *` » signifie que cette planification s’exécutera à 1 heure du matin tous les jours. |
| `children.state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont « actif » et « inactif ». Par défaut, l’état est défini sur « inactif ». |

+++

## Création d’un nouveau planning {#create}

Vous pouvez créer un nouveau planning en effectuant une requête POST au point d’entrée `/config/schedules`.

**Format d’API**

```http
POST /config/schedules
```

**Requête**

+++ Exemple de requête pour créer un planning. 

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
| `type` | **Obligatoire.** Type de tâche sous forme de chaîne. Les deux types pris en charge sont « batch_segmentation » et « export ». |
| `properties` | **Obligatoire.** Objet contenant des propriétés supplémentaires liées au planning. |
| `properties.segments` | **Obligatoire lorsque la `type` est égale à « batch_segmentation ».** L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `schedule` | *Facultatif.* Chaîne contenant le planning de la tâche. Les tâches ne peuvent être planifiées pour s’exécuter qu’une seule fois par jour, ce qui signifie que vous ne pouvez pas planifier une tâche pour qu’elle s’exécute plus d’une fois sur une période de 24 heures. Pour plus d’informations sur les plannings cron, consultez l’annexe sur le [format d’expression cron](#appendix). Dans cet exemple, « `0 0 1 * *` » signifie que cette planification s’exécutera à 1 heure du matin tous les jours. <br><br>Si cette chaîne n’est pas fournie, un planning généré par le système est automatiquement généré. |
| `state` | *Facultatif.* Chaîne contenant l’état du planning. Les deux états pris en charge sont « actif » et « inactif ». Par défaut, l’état est défini sur « inactif ». |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de votre nouveau planning.

+++ Exemple de réponse lors de la création d’un planning.

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

+++

## Récupération d’un planning spécifique {#get}

Vous pouvez récupérer des informations détaillées sur un planning spécifique en adressant une requête GET au point d’entrée `/config/schedules` et en fournissant l’identifiant du planning que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planning que vous souhaitez récupérer. |

**Requête**

+++ Exemple de requête pour récupérer un planning. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur le planning spécifié.

+++ Exemple de réponse lors de la récupération d’un planning.

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
| `type` | Type de traitement sous forme de chaîne. Les deux types pris en charge sont `batch_segmentation` et `export`. |
| `properties` | Objet contenant des propriétés supplémentaires liées au planning. |
| `properties.segments` | L’utilisation de `["*"]` garantit que tous les segments sont inclus. |
| `schedule` | Chaîne contenant le planning du traitement. Vous ne pouvez planifier qu’une seule exécution de tâche par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution d’une tâche plus d’une fois au cours d’une période de 24 heures. Pour plus d’informations sur les plannings cron, consultez l’annexe sur le [format d’expression cron](#appendix). Dans cet exemple, « `0 0 1 * *` » signifie que cette planification s’exécutera à 1 heure du matin tous les jours. |
| `state` | Chaîne contenant l’état du planning. Les deux états pris en charge sont `active` et `inactive`. Par défaut, l’état est défini sur `inactive`. |

+++

## Mettre à jour les détails d’un planning spécifique {#update}

Vous pouvez mettre à jour un planning spécifique en adressant une requête PATCH au point d’entrée `/config/schedules` et en fournissant l’identifiant du planning que vous tentez de mettre à jour dans le chemin de requête.

La requête PATCH vous permet de mettre à jour la planification [state](#update-state) ou [cron](#update-schedule) pour une planification individuelle.

**Format d’API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planning que vous souhaitez mettre à jour. |

>[!BEGINTABS]

>[!TAB Mettre à jour l’état du planning]

Vous pouvez utiliser une opération Correctif JSON pour mettre à jour l’état du planning. Pour mettre à jour l’état, vous déclarez la propriété `path` comme `/state` et définissez l’`value` sur `active` ou `inactive`. Pour plus d’informations sur le correctif JSON, consultez la documentation du [correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902).

**Requête**

+++ Exemple de requête pour mettre à jour l’état du planning.

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

+++

| Propriété | Description |
| -------- | ----------- |
| `path` | Chemin d’accès de la valeur que vous souhaitez mettre à jour. Dans ce cas, puisque vous mettez à jour l’état du planning, vous devez définir la valeur de `path` sur « /state ». |
| `value` | Valeur mise à jour de l’état du planning. Cette valeur peut être définie comme « active » ou « inactive » pour activer ou désactiver le planning. Notez que vous **ne pouvez pas** désactiver un planning si l’organisation a été activée pour la diffusion en continu. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

>[!TAB Mettre à jour le planning cron]

Vous pouvez utiliser une opération Correctif JSON pour mettre à jour la planification cron. Pour mettre à jour le planning, vous déclarez la propriété `path` comme `/schedule` et définissez la `value` sur un planning cron valide. Pour plus d’informations sur le correctif JSON, consultez la documentation du [correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902). Pour plus d’informations sur les plannings cron, consultez l’annexe sur le [format d’expression cron](#appendix).

>[!ENDTABS]

**Requête**

+++ Exemple de requête pour mettre à jour le planning.

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
| `path` | Chemin d’accès de la valeur à mettre à jour. Dans ce cas, puisque vous mettez à jour la planification cron, vous devez définir la valeur de `path` sur `/schedule`. |
| `value` | Valeur mise à jour du planning cron. Cette valeur doit se présenter sous la forme d’un planning cron. Dans cet exemple, le planning se déroulera le deuxième jour de chaque mois. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

## Suppression d’un planning spécifique

Vous pouvez demander la suppression d’un planning spécifique en adressant une requête DELETE au point d’entrée `/config/schedules` et en fournissant l’identifiant du planning que vous souhaitez supprimer du chemin de requête.

**Format d’API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SCHEDULE_ID}` | Valeur `id` du planning que vous souhaitez supprimer. |

**Requête**

+++ Exemple de requête de suppression d’un planning.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (No Content).

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux le fonctionnement des plannings.

## Annexe {#appendix}

L’annexe suivante explique le format des expressions cron utilisées dans les plannings.

### Format

Une expression cron est une chaîne composée de 6 ou 7 champs. L’expression se présente comme suit :

`0 0 12 * * ?`

Dans une chaîne d’expression cron, le premier champ représente les secondes, le second les minutes, le troisième les heures, le quatrième le jour du mois, le cinquième le mois et le sixième le jour de la semaine. Vous pouvez également inclure éventuellement un septième champ, qui représente l’année.

| Nom du champ | Obligatoire | Valeurs possibles | Caractères spéciaux autorisés |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Oui | 0-59 | `, - * /` |
| Minutes | Oui | 0-59 | `, - * /` |
| Heures | Oui | 0-23 | `, - * /` |
| Jour du mois | Oui | 1-31 | `, - * ? / L W` |
| Month | Oui | 1ER-12 JANVIER-DÉCEMBRE | `, - * /` |
| Jour de la semaine | Oui | 1-7, SUN-SAM | `, - * ? / L #` |
| Year | Non | Vide, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Les noms des mois et des jours de la semaine ne respectent **pas** la casse. Par conséquent, `SUN` équivaut à utiliser `sun`.

Les caractères spéciaux autorisés ont la signification suivante :

| Caractère spécial | Description |
| ----------------- | ----------- |
| `*` | Cette valeur est utilisée pour sélectionner **toutes** les valeurs d’un champ. Par exemple, l’ajout de `*` dans le champ heures signifierait **toutes les** heures. |
| `?` | Cette valeur signifie qu’aucune valeur spécifique n’est requise. Ceci est généralement utilisé pour spécifier quelque chose dans un champ où le caractère est autorisé, mais pas dans l’autre. Par exemple, si vous souhaitez qu’un événement soit déclenché tous les trois du mois, mais que vous ne vous souciez pas du jour de la semaine, vous devez `3` dans le champ jour du mois et `?` dans le champ jour de la semaine. |
| `-` | Cette valeur est utilisée pour spécifier des plages **inclusives** pour le champ. Par exemple, si vous placez `9-15` dans le champ heures, cela signifie que les heures incluent 9, 10, 11, 12, 13, 14 et 15. |
| `,` | Cette valeur est utilisée pour spécifier des valeurs supplémentaires. Par exemple, si vous placez `MON, FRI, SAT` dans le champ jour de la semaine , cela signifie que les jours de la semaine incluent le lundi, le vendredi et le samedi. |
| `/` | Cette valeur est utilisée pour spécifier des incréments. La valeur placée avant le `/` détermine l’endroit à partir duquel il incrémente, tandis que la valeur placée après le `/` détermine son incrémentation. Par exemple, si vous mettez `1/7` dans le champ des procès-verbaux, cela signifie que les procès-verbaux comprendraient 1, 8, 15, 22, 29, 36, 43, 50 et 57. |
| `L` | Cette valeur est utilisée pour spécifier `Last` et a une signification différente selon le champ par lequel elle est utilisée. S’il est utilisé avec le champ Jour du mois, il représente le dernier jour du mois. S’il est utilisé seul avec le champ Jour de la semaine, il représente le dernier jour de la semaine, à savoir samedi (`SAT`). S’il est utilisé avec le champ Jour de la semaine, en conjonction avec une autre valeur, il représente le dernier jour de ce type pour le mois. Par exemple, si vous placez `5L` dans le champ jour de la semaine, cela **uniquement** inclure le dernier vendredi du mois. |
| `W` | Cette valeur est utilisée pour spécifier le jour de la semaine le plus proche du jour donné. Par exemple, si vous placez `18W` dans le champ jour du mois, et que le 18 de ce mois était un samedi, cela se déclencherait le vendredi 17, qui est le jour de la semaine le plus proche. Si le 18 de ce mois-là était un dimanche, cela se déclencherait le lundi 19, qui est le jour de la semaine le plus proche. Veuillez noter que si vous placez `1W` dans le champ jour du mois et que le jour de la semaine le plus proche se trouve dans le mois précédent, l’événement se déclenchera toujours le jour de la semaine le plus proche du **mois en cours**.</br></br>De plus, vous pouvez combiner des `L` et des `W` pour effectuer des `LW`, ce qui spécifie le dernier jour de la semaine du mois. |
| `#` | Cette valeur est utilisée pour spécifier le énième jour de la semaine dans un mois. La valeur placée avant le `#` représente le jour de la semaine, tandis que la valeur placée après le `#` représente l’occurrence du mois en question. Par exemple, si vous placez `1#3`, l’événement se déclenche le troisième dimanche du mois. Veuillez noter que si vous mettez `X#5` et qu’il n’y a pas de cinquième occurrence de ce jour de la semaine dans ce mois-là, l’événement **sera pas déclenché** Par exemple, si vous mettez `1#5` et qu’il n’y a pas de cinquième dimanche dans ce mois-là, l’événement **sera pas déclenché** |

### Exemples

Le tableau suivant présente des exemples de chaînes d’expression cron et explique ce qu’elles signifient.

| Expression | Explication |
| ---------- | ----------- |
| `0 0 13 * * ?` | L&#39;événement se déclenchera à 13h tous les jours. |
| `0 30 9 * * ? 2022` | L’événement se déclenchera tous les jours à 9 :30AM en 2022. |
| `0 * 18 * * ?` | L’événement se déclenchera toutes les minutes, à partir de 18h00 et se terminera à 18:59PM, tous les jours. |
| `0 0/10 17 * * ?` | L&#39;événement se déclenchera toutes les 10 minutes, à partir de 17h et se terminera à 18h, tous les jours. |
| `0 13,38 5 ? 6 WED` | L&#39;événement se déclenchera à 5 :13AM et 5 :38AM tous les mercredis de juin. |
| `0 30 12 ? * 4#3` | L&#39;événement se déclenchera à 12 :30PM le troisième mercredi de chaque mois. |
| `0 30 12 ? * 6L` | L&#39;événement se déclenchera à 12 :30PM le dernier vendredi de chaque mois. |
| `0 45 11 ? * MON-THU` | L&#39;événement se déclenchera à 11 :45AM tous les lundis, mardis, mercredis et jeudis. |