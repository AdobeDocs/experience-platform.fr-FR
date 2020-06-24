---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation en flux continu
topic: developer guide
translation-type: tm+mt
source-git-commit: d00973a07c5fb137f756040fb1dc6eac5a1630f5
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 1%

---


# Évaluer les événements en temps quasi réel avec la segmentation en flux continu

>[!NOTE] Le document suivant indique comment utiliser la segmentation en flux continu à l’aide de l’API. Pour plus d’informations sur l’utilisation de la segmentation en flux continu à l’aide de l’interface utilisateur, consultez le guide [du créateur de](../ui/overview.md#streaming-segmentation)segments.

La segmentation en flux continu sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer la segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit désormais lorsque les données entrent en [!DNL Platform]jeu, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure que les données sont transmises [!DNL Platform], ce qui signifie que l’appartenance à un segment est mise à jour sans exécuter de tâches de segmentation planifiées.

![](../images/api/streaming-segment-evaluation.png)

## Prise en main

Ce guide du développeur nécessite une bonne compréhension des différents [!DNL Adobe Experience Platform] services impliqués dans la segmentation en flux continu. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [!DNL Real-time Customer Profile](../../profile/home.md): Fournit un profil unifié pour les consommateurs en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [!DNL Segmentation](../home.md): Permet de créer des segments et des audiences à partir de vos [!DNL Real-time Customer Profile] données.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer [!DNL Platform] les API.

### Lecture des exemples d’appels d’API

Ce guide du développeur fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de [!DNL Experience Platform] dépannage.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux [!DNL Platform] API, vous devez d&#39;abord suivre le didacticiel [d&#39;](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’ [!DNL Experience Platform] API, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées à des sandbox virtuels spécifiques. Toutes les requêtes aux [!DNL Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans [!DNL Platform], voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

Des en-têtes supplémentaires peuvent être nécessaires pour exécuter des requêtes spécifiques. Les en-têtes corrects sont affichés dans chacun des exemples de ce document. Veuillez prêter une attention particulière aux exemples de demandes afin de vous assurer que tous les en-têtes requis sont inclus.

### Types de requêtes activés pour la segmentation en flux continu {#streaming-segmentation-query-types}

>[!NOTE] Vous devez activer la segmentation planifiée pour l’organisation afin que la segmentation en flux continu fonctionne. Vous trouverez des informations sur l’activation de la segmentation planifiée dans la section [Activer la segmentation planifiée.](#enable-scheduled-segmentation)

Pour qu’un segment soit évalué à l’aide de la segmentation en flux continu, la requête doit se conformer aux directives suivantes.

| Type de Requête | Détails |
| ---------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. |
| Accès entrant dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant **au cours des sept derniers jours**. |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. |
| Accès entrant faisant référence à un profil dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant et à un ou plusieurs attributs de profil, **au cours des sept derniers jours**. |
| Plusieurs événements faisant référence à un profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. |

La section suivante liste des exemples de définition de segment qui **ne seront pas** activés pour la segmentation en flux continu.

| Type de Requête | Détails |
| ---------- | ------- | 
| Accès entrant dans une fenêtre de temps relative | Si la définition de segment fait référence à un événement entrant **qui ne se trouve pas** dans la **dernière période** de sept jours. Par exemple, au cours des deux **dernières semaines**. |
| Accès entrant faisant référence à un profil dans une fenêtre relative | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>événement entrant **non** compris dans la **dernière période** de sept jours.</li><li>Définition de segment qui comprend des segments ou des caractéristiques d’Adobe Audience Manager (AAM).</li></ul> |
| Plusieurs événements faisant référence à un profil | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>événement qui **ne se produit pas** au cours **des dernières 24 heures**.</li><li>Définition de segment qui comprend des segments ou des caractéristiques d’Adobe Audience Manager (AAM).</li></ul> |
| requêtes multientité | Les requêtes multientités **ne sont pas** prises en charge dans leur ensemble par la segmentation en flux continu. |

En outre, certaines directives s’appliquent lors de la segmentation en flux continu :

| Type de Requête | Ligne directrice |
| ---------- | -------- |
| requête événement unique | La fenêtre de rétrospective est limitée à **sept jours**. |
| Requête avec historique des événements | <ul><li>La fenêtre de rétrospective est limitée à **un jour**.</li><li>Une condition d’ordre temporel strict **doit** exister entre les événements.</li><li>Seules les commandes de temps simples (avant et après) entre les événements sont autorisées.</li><li>Les événements individuels **ne peuvent** être annulés. Cependant, toute la requête **peut** être annulée.</li></ul> |

## Récupérer tous les segments activés pour la segmentation en flux continu

Vous pouvez récupérer une liste de tous vos segments qui sont activés pour la segmentation en flux continu au sein de votre organisation IMS en envoyant une requête GET au point de `/segment/definitions` terminaison.

**Format d’API**

Pour récupérer les segments activés pour la diffusion en continu, vous devez inclure le paramètre de requête `evaluationInfo.continuous.enabled=true` dans le chemin d’accès à la requête.

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

Une réponse réussie renvoie un tableau de segments de votre organisation IMS qui sont activés pour la segmentation en flux continu.

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

## Création d’un segment compatible avec la diffusion en continu

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

>[!NOTE] Il s’agit d’une requête standard &quot;créer un segment&quot;. Pour plus d&#39;informations sur la création d&#39;une définition de segment, consultez le didacticiel sur la [création d&#39;un segment](../tutorials/create-a-segment.md).

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle définition de segment activée pour la diffusion en continu.

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

## Activer l’évaluation planifiée {#enable-scheduled-segmentation}

Une fois l’évaluation en flux continu activée, une ligne de base doit être créée (après quoi le segment sera toujours à jour). L’évaluation planifiée (également appelée segmentation planifiée) doit d’abord être activée pour que le système puisse exécuter automatiquement le nettoyage. Avec la segmentation planifiée, votre organisation IMS peut respecter un calendrier récurrent pour exécuter automatiquement des tâches d’exportation afin d’évaluer les segments.

>[!NOTE] L’évaluation planifiée peut être activée pour les sandbox avec un maximum de cinq (5) stratégies de fusion pour un Profil XDM individuel. Si votre entreprise dispose de plus de cinq stratégies de fusion pour un Profil XDM individuel au sein d’un seul environnement de sandbox, vous ne pourrez pas utiliser l’évaluation planifiée.

### Créer un calendrier

En adressant une requête POST au point de `/config/schedules` terminaison, vous pouvez créer une planification et inclure l&#39;heure spécifique à laquelle la planification doit être déclenchée.

**Format d’API**

```http
POST /config/schedules
```

**Requête**

La demande suivante crée un nouveau calendrier en fonction des spécifications fournies dans la charge utile.

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
| `name` | **(Obligatoire)** Nom de la planification. Doit être une chaîne. |
| `type` | **(Obligatoire)** Type de tâche au format chaîne. Les types pris en charge sont `batch_segmentation` et `export`. |
| `properties` | **(Obligatoire)** Objet contenant des propriétés supplémentaires liées à la planification. |
| `properties.segments` | **(Obligatoire lorsque`type`est égal`batch_segmentation`)** L’utilisation `["*"]` de cette option garantit l’inclusion de tous les segments. |
| `schedule` | **(Obligatoire)** Chaîne contenant la planification de la tâche. Les tâches ne peuvent être planifiées qu’une fois par jour, ce qui signifie que vous ne pouvez pas planifier une tâche pour qu’elle s’exécute plusieurs fois au cours d’une période de 24 heures. L&#39;exemple illustré (`0 0 1 * * ?`) signifie que la tâche est déclenchée tous les jours à 1:00:00 UTC. Pour plus d’informations, consultez la documentation sur le format [d’expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. |
| `state` | *(Facultatif)* Chaîne contenant l&#39;état de planification. Valeurs disponibles : `active` et `inactive`. La valeur par défaut est `inactive`. Une organisation IMS ne peut créer qu&#39;une seule planification. Les étapes de mise à jour du calendrier sont disponibles plus loin dans ce didacticiel. |

**Réponse**

Une réponse positive renvoie les détails du nouveau planning.

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

### Activation d’une planification

Par défaut, une planification est inactive lors de sa création, sauf si la `state` propriété est définie sur `active` dans le corps de la demande de création (POST). Vous pouvez activer une planification (définissez la `state` sur `active`) en exécutant une requête PATCH sur le point de `/config/schedules` terminaison et en incluant l&#39;ID de la planification dans le chemin d&#39;accès.

**Format d’API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Requête**

La requête suivante utilise la mise en forme [des correctifs](http://jsonpatch.com/) JSON pour mettre à jour `state` la planification sur `active`.

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

Une mise à jour réussie renvoie un corps de réponse vide et un état HTTP 204 (aucun contenu).

La même opération peut être utilisée pour désactiver une planification en remplaçant la &quot;valeur&quot; de la requête précédente par &quot;inactive&quot;.

## Étapes suivantes

Maintenant que vous avez activé à la fois les segments nouveaux et existants pour la segmentation en flux continu et activé la segmentation planifiée pour développer une base de référence et effectuer des évaluations périodiques, vous pouvez commencer à créer des segments pour votre organisation.

Pour savoir comment exécuter des actions similaires et utiliser des segments à l’aide de l’interface utilisateur de l’Adobe Experience Platform, consultez le guide [d’utilisation du créateur de](../ui/overview.md)segments.