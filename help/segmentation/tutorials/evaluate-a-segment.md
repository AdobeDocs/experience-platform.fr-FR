---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Évaluer un segment
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 2%

---


# Évaluer et accéder aux résultats des segments

Ce document fournit un didacticiel pour évaluer les segments et accéder aux résultats des segments à l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation.

## Prise en main

Ce didacticiel nécessite une bonne compréhension des différents services d’Adobe Experience Platform impliqués dans la création de segments d’audience. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Profil](../../profile/home.md)client en temps réel : Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Service](../home.md)de segmentation des Adobes Experience Platform : Permet de créer des segments d’audience à partir des données du Profil client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

### En-têtes requis

Ce didacticiel nécessite également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin de pouvoir invoquer les API Platform. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l&#39;Experience Platform sont isolées dans des sandbox virtuels spécifiques. Les requêtes aux API Platform nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes POST, PUT et PATCH nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Évaluer un segment

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment par le biais d’une évaluation planifiée ou d’une évaluation à la demande.

[L’évaluation](#scheduled-evaluation) planifiée (également appelée &quot;segmentation planifiée&quot;) vous permet de créer un calendrier récurrent pour l’exécution d’une tâche d’exportation à un moment donné, tandis que l’évaluation [à la](#on-demand-evaluation) demande implique la création d’une tâche de segment afin de créer l’audience immédiatement. Les étapes pour chacun d&#39;eux sont décrites ci-dessous.

Si vous n’avez pas encore terminé la procédure [Créer un segment à l’aide du didacticiel API](./create-a-segment.md) de Profil client en temps réel ou créé une définition de segment à l’aide du créateur [de](../ui/overview.md)segments, veuillez le faire avant de continuer ce didacticiel.

## Évaluation programmée {#scheduled-evaulation}

Grâce à une évaluation planifiée, votre organisation IMS peut créer un calendrier récurrent pour exécuter automatiquement les tâches d’exportation.

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

### Mettre à jour l&#39;heure de planification

La planification peut être mise à jour en envoyant une requête PATCH au point de `/config/schedules` terminaison et en incluant l&#39;ID de la planification dans le chemin.

**Format d’API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Requête**

La requête suivante utilise la mise en forme [des correctifs](http://jsonpatch.com/) JSON afin de mettre à jour l’expression [](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron pour la planification. Dans cet exemple, la planification est maintenant déclenchée à 10h15 UTC.

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
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Réponse**

Une mise à jour réussie renvoie un corps de réponse vide et un état HTTP 204 (aucun contenu).

## Évaluation à la demande

L’évaluation à la demande vous permet de créer une tâche de segment afin de générer un segment d’audience chaque fois que vous en avez besoin. Contrairement à l&#39;évaluation planifiée, cela n&#39;aura lieu que lorsque cela est demandé et n&#39;est pas récurrent.

### Création d’une tâche de segment

Une tâche de segment est un processus asynchrone qui crée un segment d’audience. Il fait référence à une définition de segment, ainsi qu’à toute stratégie de fusion contrôlant la manière dont le Profil client en temps réel fusionne des attributs qui se chevauchent dans vos fragments de profil. Une fois la tâche de segmentation terminée, vous pouvez collecter diverses informations sur le segment, telles que les erreurs qui se sont produites au cours du traitement et la taille finale de votre audience.

Vous pouvez créer une tâche de segment en adressant une requête POST au point de `/segment/jobs` terminaison dans l’API Profil client en temps réel.

**Format d’API**

```http
POST /segment/jobs
```

**Requête**

La requête suivante crée une tâche de segment basée sur les deux définitions de segment fournies dans la charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Propriété | Description |
| -------- | ----------- |
| `segmentId` | Identificateur d’une définition de segment à partir de laquelle créer l’audience. Au moins un ID de segment doit être fourni dans le tableau de charge utile. |

**Réponse**

Une réponse positive renvoie les détails de la tâche de segment nouvellement créée, y compris sa valeur `id`, en lecture seule et générée par le système, qui est unique à cette tâche de segment.

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identificateur de la nouvelle tâche de segment, utilisé à des fins de recherche. |
| `status` | Statut actuel de la tâche de segment. Sera &quot;TRAITEMENT&quot; jusqu’à ce que le traitement soit terminé, auquel moment il devient &quot;SUCCÈS&quot; ou &quot;ÉCHEC&quot;. |

### Rechercher l&#39;état de la tâche de segment

Vous pouvez utiliser le `id` pour une tâche de segment spécifique pour effectuer une demande de recherche (GET) afin de vue de l’état actuel de la tâche.

**Format d’API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | La tâche `id` du segment à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse positive renvoie les détails de la tâche de segmentation et fournit des informations différentes en fonction de l’état actuel de la tâche. Vous pouvez répéter la demande de recherche jusqu’à ce que le `status` segment atteigne &quot;SUCCEEDED&quot;, ce qui vous permet d’exporter le segment dans un jeu de données.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `segmentedProfileCounter` | Nombre total de profils fusionnés remplissant les conditions requises pour le segment. |
| `segmentedProfileByNamespaceCounter` | Ventilation des profils admissibles pour le segment par code d’espace de nommage d’identité. Une liste des codes d&#39;espace de nommage d&#39;identité se trouve dans la présentation [de l&#39;espace de nommage](../../identity-service/namespaces.md)d&#39;identité. |

## Interprétation des résultats des segments

Lorsque les tâches de segmentation sont exécutées avec succès, le `segmentMembership` mappage est mis à jour pour chaque profil inclus dans le segment. `segmentMembership` stocke également tous les segments d’audience préévalués qui sont ingérés dans Platform, ce qui permet l’intégration à d’autres solutions telles que l’Adobe Audience Manager.

L&#39;exemple suivant montre à quoi ressemble l&#39;attribut pour chaque enregistrement de profil individuel : `segmentMembership`

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propriété | Description |
| -------- | ----------- |
| `lastQualificationTime` | Horodatage au moment où l’assertion d’appartenance au segment a été faite et où le profil a saisi ou quitté le segment. |
| `status` | Statut de la participation au segment dans le cadre de la demande en cours. Doit être égal à l’une des valeurs connues suivantes : <ul><li>`existing`: L&#39;entité continue d&#39;être dans le segment.</li><li>`realized`: L&#39;entité entre dans le segment.</li><li>`exited`: L’entité quitte le segment.</li></ul> |

## Accès aux résultats du segment

Les résultats d’une tâche de segmentation sont accessibles de deux manières : vous pouvez accéder à des profils individuels ou exporter une audience entière dans un jeu de données.

Les sections suivantes décrivent ces options de manière plus détaillée.

## Rechercher un profil

Si vous connaissez le profil spécifique auquel vous souhaitez accéder, vous pouvez le faire à l’aide de l’API Profil client en temps réel. Les étapes complètes pour accéder à des profils individuels sont disponibles dans les données du Profil client en temps réel [Access à l’aide du didacticiel sur l’API](../../profile/api/entities.md) de Profil.

## Exportation d’un segment {#export}

Une fois la tâche de segmentation terminée (la valeur de l’ `status` attribut est &quot;SUCCEEDED&quot;), vous pouvez exporter votre audience dans un jeu de données où elle est accessible et où vous pouvez agir.

Pour exporter votre audience, procédez comme suit :

- [Créer un jeu de données](#create-a-target-dataset) de cible : créez le jeu de données pour contenir les membres d&#39;audience.
- [Générer des profils d&#39;audience dans le jeu de données](#generate-profiles-for-audience-members) : renseignez le jeu de données avec des Profils individuels XDM en fonction des résultats d&#39;une tâche de segment.
- [Suivre la progression](#monitor-export-progress) de l&#39;exportation - Vérifier la progression actuelle du processus d&#39;exportation.
- [Lire les données](#next-steps) d&#39;audience - Récupérez les Profils individuels XDM résultants représentant les membres de votre audience.

### Création d’un jeu de données de cible

Lors de l’exportation d’une audience, un jeu de données de cible doit d’abord être créé. Il est important que le jeu de données soit correctement configuré pour garantir la réussite de l&#39;exportation.

L’une des principales considérations à prendre en compte est le schéma sur lequel repose le jeu de données (`schemaRef.id` dans l’exemple de demande d’API ci-dessous). Pour exporter un segment, le jeu de données doit être basé sur le Schéma d&#39;Union de Profil individuel XDM (`https://ns.adobe.com/xdm/context/profile__union`). Un schéma d’union est un schéma généré par le système et en lecture seule qui agrégat les champs des schémas qui partagent la même classe, dans ce cas la classe de Profil XDM Individuel. Pour plus d&#39;informations sur les schémas des vues d&#39;union, consultez la section Profil client en temps [réel du guide](../../xdm/api/getting-started.md)de développement du registre des Schémas.

Il existe deux façons de créer le jeu de données nécessaire :

- **Utilisation des API :** Les étapes suivantes de ce didacticiel expliquent comment créer un jeu de données qui référence le Schéma d&#39;Union d&#39;Profil individuel XDM à l&#39;aide de l&#39;API Catalog.
- **Utilisation de l’interface utilisateur :** Pour utiliser l’interface utilisateur de l’Adobe Experience Platform pour créer un jeu de données faisant référence au schéma d’union, suivez les étapes du didacticiel [](../ui/overview.md) IU, puis revenez à ce didacticiel pour passer à la procédure de [génération de profils](#generate-xdm-profiles-for-audience-members)d’audience.

Si vous disposez déjà d’un jeu de données compatible et connaissez son ID, vous pouvez passer directement à l’étape de [génération de profils](#generate-xdm-profiles-for-audience-members)d’audience.

**Format d’API**

```http
POST /dataSets
```

**Requête**

La requête suivante crée un nouveau jeu de données, fournissant des paramètres de configuration dans la charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom descriptif du jeu de données. |
| `schemaRef.id` | ID de la vue d&#39;union (schéma) à laquelle le jeu de données sera associé. |
| `fileDescription.persisted` | Valeur booléenne qui, lorsqu’elle est définie sur `true`, permet au jeu de données de persister dans la vue d’union. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;identifiant unique généré par le système et en lecture seule du jeu de données nouvellement créé. Un ID de jeu de données correctement configuré est nécessaire pour exporter les membres d&#39;audience.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Générer des profils pour les membres d’audience

Une fois que vous disposez d’un jeu de données persistant en union, vous pouvez créer une tâche d’exportation afin de conserver les membres de l’audience dans le jeu de données en envoyant une requête POST au point de `/export/jobs` terminaison dans l’API Profil client en temps réel et en fournissant l’ID du jeu de données et les informations de segment pour les segments que vous souhaitez exporter.

**Format d’API**

```http
POST /export/jobs
```

**Requête**

La demande suivante crée une nouvelle tâche d’exportation, fournissant des paramètres de configuration dans la charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `fields` | *(Facultatif)* Limite les champs de données à inclure dans l’exportation à ceux fournis dans ce paramètre. Le même paramètre est également disponible lors de la création d’un segment. Par conséquent, les champs du segment ont peut-être déjà été filtrés. Si cette valeur est omise, tous les champs seront inclus dans les données exportées. |
| `mergePolicy` | *(Facultatif)* Spécifie la stratégie de fusion pour régir les données exportées. Incluez ce paramètre lorsqu’il existe plusieurs segments exportés. Si cette valeur est omise, le service d’exportation utilisera la stratégie de fusion fournie par le segment. |
| `mergePolicy.id` | ID de la stratégie de fusion |
| `mergePolicy.version` | Version spécifique de la stratégie de fusion à utiliser. Si vous omettez cette valeur, la version la plus récente sera utilisée par défaut. |
| `filter` | *(Facultatif)* Spécifie un ou plusieurs des filtres suivants à appliquer au segment avant l’exportation : |
| `filter.segments` | *(Facultatif)* Indique les segments à exporter. Si cette valeur est omise, toutes les données de tous les profils seront exportées. Accepte un tableau d’objets de segment, chacun contenant les champs suivants : |
| `filter.segments.segmentId` | **(Obligatoire en cas d’utilisation`segments`)** Identifiant de segment pour les profils à exporter. |
| `filter.segments.segmentNs` | *(Facultatif)* Segmenter l’espace de nommage pour le segment donné `segmentID`. |
| `filter.segments.status` | *(Facultatif)* Tableau de chaînes fournissant un filtre d’état pour le `segmentID`. Par défaut, `status` aura la valeur `["realized", "existing"]` qui représente tous les profils qui tombent dans le segment à l’heure actuelle. Les valeurs possibles sont les suivantes : `"realized"`, `"existing"`et `"exited"`. |
| `filter.segmentQualificationTime` | *(Facultatif)* Filtrer en fonction de l’heure de qualification du segment. L’heure de début et/ou l’heure de fin peuvent être fournies. |
| `filter.segmentQualificationTime.startTime` | *(Facultatif)* Heure de début de qualification des segments pour un ID de segment pour un état donné. Il n’est pas fourni, il n’y aura aucun filtre sur l’heure de début pour une qualification d’ID de segment. L&#39;horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Facultatif)* Heure de fin de qualification de segment pour un ID de segment pour un état donné. Il n’est pas fourni, il n’y aura pas de filtre à l’heure de fin pour une qualification d’ID de segment. L&#39;horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` | *(Facultatif)* Limite les profils exportés à inclure uniquement ceux qui ont été mis à jour après cet horodatage. L&#39;horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` pour les **profils**, le cas échéant | Inclut tous les profils fusionnés où l’horodatage mis à jour fusionné est supérieur à l’horodatage donné. Prend en charge `greater_than` l’opérande. |
| `filter.fromTimestamp` pour événements | Tous les événements ingérés après cet horodatage seront exportés correspondant au résultat du profil obtenu. Ce n&#39;est pas le temps de événement lui-même, mais le temps d&#39;assimilation des événements. |
| `filter.emptyProfiles` | *(Facultatif)* Valeur booléenne. Les Profils peuvent contenir des enregistrements de Profil, des enregistrements ExperienceEvent ou les deux. Les Profils sans enregistrement de Profil et seuls les enregistrements ExperienceEvent sont appelés &quot;profils vides&quot;. Pour exporter tous les profils de la banque de Profils, y compris les &quot;profils vides&quot;, définissez la valeur de `emptyProfiles` sur `true`. Si `emptyProfiles` est défini sur `false`, seuls les profils contenant des enregistrements de Profil dans la boutique sont exportés. Par défaut, si `emptyProfiles` l’attribut n’est pas inclus, seuls les profils contenant des enregistrements de Profil sont exportés. |
| `additionalFields.eventList` | *(Facultatif)* Contrôle les champs de événement de série chronologique exportés pour des objets enfants ou associés en fournissant un ou plusieurs des paramètres suivants : |
| `additionalFields.eventList.fields` | Contrôlez les champs à exporter. |
| `additionalFields.eventList.filter` | Indique les critères qui limitent les résultats inclus dans les objets associés. Attend une valeur minimale requise pour l’exportation, généralement une date. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Filtres les événements de série chronologique à ceux qui ont été ingérés après l’horodatage fourni. Ce n&#39;est pas le temps de événement lui-même, mais le temps d&#39;assimilation des événements. |
| `destination` | **(Obligatoire)** Informations de destination pour les données exportées |
| `destination.datasetId` | **(Obligatoire)** ID du jeu de données dans lequel les données doivent être exportées. |
| `destination.segmentPerBatch` | *(Facultatif)* Valeur booléenne qui, si elle n’est pas fournie, prend par défaut la valeur `false`. Une valeur de `false` exporte tous les ID de segment dans un seul ID de lot. Une valeur de `true` exporte un ID de segment dans un ID de lot. Notez que la définition de la valeur `true` peut affecter les performances d’exportation par lot. |
| `schema.name` | **(Obligatoire)** Nom du schéma associé au jeu de données dans lequel les données doivent être exportées. |

**Réponse**

Une réponse réussie renvoie un jeu de données rempli avec des profils qualifiés pour la dernière exécution terminée du travail de segment. Les profils qui existaient peut-être auparavant dans le jeu de données mais n’étaient pas inclus dans le segment au cours de la dernière exécution terminée du travail de segment ont été supprimés.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Si `destination.segmentPerBatch` la requête n’avait pas été incluse (si elle n’était pas présente, elle est définie par défaut `false`) ou si la valeur avait été définie sur `false`, l’objet `destination` de la réponse ci-dessus ne contiendrait pas de tableau et inclurait à la place un seul `batches` `batchId`tableau, comme illustré ci-dessous. Ce lot unique inclurait tous les ID de segment, alors que la réponse ci-dessus montre un identifiant de segment unique par ID de lot.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Liste de toutes les tâches d’exportation

Vous pouvez renvoyer une liste de toutes les tâches d’exportation pour une organisation IMS particulière en exécutant une demande GET au point de `export/jobs` terminaison. La demande prend également en charge les paramètres de requête `limit` et `offset`, comme indiqué ci-dessous.

**Format d’API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propriété | Description |
| -------- | ----------- |
| `limit` | Spécifiez le nombre d&#39;enregistrements à renvoyer. |
| `offset` | Décale la page de résultats à renvoyer par le nombre fourni. |


**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend un `records` objet contenant les tâches d’exportation créées par votre organisation IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Suivi de la progression de l&#39;exportation

En tant que processus d’exportation, vous pouvez contrôler son état en envoyant une requête GET au point de `/export/jobs` terminaison et en incluant la tâche `id` d’exportation dans le chemin. La tâche d’exportation est terminée une fois que le `status` champ renvoie la valeur &quot;SUCCEEDED&quot;.

**Format d’API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | La tâche `id` d’exportation à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propriété | Description |
| -------- | ----------- |
| `batchId` | Identifiant des lots créés à partir d&#39;une exportation réussie, à utiliser à des fins de recherche lors de la lecture des données d&#39;audience. |

## Étapes suivantes

Une fois l’exportation terminée, vos données sont disponibles dans Data Lake en Experience Platform. Vous pouvez ensuite utiliser l’API [d’accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) données pour accéder aux données à l’aide de l’API `batchId` associée à l’exportation. En fonction de la taille du segment, les données peuvent se trouver en blocs et le lot peut se composer de plusieurs fichiers.

Pour obtenir des instructions détaillées sur l’utilisation de l’API d’accès aux données pour accéder aux fichiers de commandes et les télécharger, suivez le didacticiel [Accès aux](../../data-access/tutorials/dataset-data.md)données.

Vous pouvez également accéder aux données de segment exportées avec succès à l’aide d’Adobe Experience Platform Requête Service. Grâce à l’interface utilisateur ou à l’API RESTful, Requête Service vous permet d’écrire, de valider et d’exécuter des requêtes sur des données du lac Data.

Pour plus d&#39;informations sur la manière de requête des données d&#39;audience, consultez la documentation [de](../../query-service/home.md)Requête Service.
