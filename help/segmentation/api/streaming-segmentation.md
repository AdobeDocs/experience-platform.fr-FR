---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation en flux continu
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 2%

---


# Évaluer les événements en temps réel avec la segmentation en flux continu (bêta)

>[!NOTE] La segmentation en flux continu est une fonctionnalité bêta qui sera disponible sur demande.

La segmentation en flux continu (également appelée évaluation continue de la requête) permet d’évaluer instantanément un client dès qu’un événement entre dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à Adobe Experience Platform, ce qui signifie que l’appartenance à un segment est mise à jour sans exécuter les tâches de segmentation planifiées.

![](../images/api/streaming-segment-evaluation.png)

## Prise en main

Ce guide du développeur nécessite une bonne compréhension des différents services Adobe Experience Platform impliqués dans la segmentation en flux continu. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Profil](../../profile/home.md)client en temps réel : Fournit un profil unifié pour les consommateurs en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Segmentation](../home.md): Permet de créer des segments et des audiences à partir de vos données de Profil client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API de plateforme.

### Lecture des exemples d’appels d’API

Ce guide du développeur fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

Des en-têtes supplémentaires peuvent être nécessaires pour exécuter des requêtes spécifiques. Les en-têtes corrects sont affichés dans chacun des exemples de ce document. Veuillez prêter une attention particulière aux exemples de demandes afin de vous assurer que tous les en-têtes requis sont inclus.

### Types de requêtes activés pour la segmentation en flux continu

Le tableau suivant liste les différents types de requêtes de segmentation et indique si elles prennent en charge ou non la segmentation en flux continu.

| Type de Requête | Exemple de requête | Segmentation en flux continu prise en charge |
| ---------- | ------------ | --------------------------------- |
| Données démographiques simples | &quot;Donnez-moi toutes les personnes dont l&#39;adresse est au Canada.&quot; | Pris en charge |
| événements de séries chronologiques | &quot;Donnez-moi toutes les personnes qui ont téléchargé Lightroom.&quot; | Pris en charge |
| Données démographiques et séries chronologiques | &quot;Donnez-moi tous ceux qui vivent au Canada et qui ont passé commande au cours des 30 derniers jours.&quot; | Pris en charge |
| Absence de événements | &quot;Donnez-moi tous ceux qui ont abandonné deux chariots séparés dans les deux jours qui suivent.&quot; | Pris en charge |
| Multi-entité | &quot;Donnez-moi toutes les personnes dont le type de droits est &quot;Expérimenté&quot;.&quot; | Non pris en charge |
| Fonctions PQL avancées | &quot;Donnez-moi tous les profils qui ont passé une commande la semaine dernière, et incluez le SKU et le nom de tous les produits achetés.&quot; | Non pris en charge |

## Récupérer tous les segments activés pour la segmentation en flux continu

Avant de créer un segment compatible avec la diffusion en continu ou de mettre à jour un segment existant pour qu’il soit compatible avec la diffusion en continu, veillez à ne pas dupliquer les informations en récupérant une liste de tous les segments compatibles avec la diffusion en continu.

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

Après avoir confirmé que le segment que vous souhaitez créer n’existe pas déjà, vous pouvez créer un nouveau segment qui est activé pour la segmentation en flux continu.

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

La requête suivante crée un segment pour lequel la segmentation en flux continu est activée. Note that the `continuous` section is set to `enabled: true`.

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
    }
}'
```

>[!NOTE] Il s’agit d’une requête standard &quot;créer un segment&quot;, avec le paramètre ajouté de la `continuous` section défini sur `enabled: true`. Pour plus d&#39;informations sur la création d&#39;une définition de segment, consultez la documentation sur la création [de](../tutorials/create-a-segment.md)segment.

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

## Activation d’un segment existant pour la segmentation en flux continu

Vous pouvez activer un segment existant pour la segmentation en flux continu en fournissant l’ID de la définition de segment dans le chemin d’une requête PATCH. En outre, la charge utile de cette demande PATCH doit inclure tous les détails de la définition de segment existante, accessible en adressant une demande GET à la définition de segment en question.

### Rechercher une définition de segment existante

Pour rechercher une définition de segment existante, vous devez indiquer son identifiant dans le chemin d’une requête GET.

**Format d’API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID de la définition de segment que vous souhaitez rechercher. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renverra les détails de la définition de segment que vous avez demandée.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] Pour la prochaine requête, vous aurez besoin des détails complets de la définition de segment qui ont été renvoyés dans cette réponse. Veuillez copier les détails de cette réponse à utiliser dans le corps de la requête suivante.

### Activer le segment existant pour la segmentation en flux continu

Maintenant que vous connaissez les détails du segment que vous souhaitez mettre à jour, vous pouvez exécuter une requête PATCH pour mettre à jour le segment afin d’activer la segmentation en flux continu.

**Format d’API**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Requête**

La charge utile de la requête suivante fournit les détails de la définition de segment (obtenue à l’étape [](#look-up-an-existing-segment-definition)précédente) et la met à jour en modifiant sa `continuous.enabled` propriété en `true`conséquence.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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
    }
}'
```

**Réponse**

Une réponse positive renvoie les détails de la définition de segment nouvellement mise à jour.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Activer l’évaluation planifiée

Une fois l’évaluation en flux continu activée, une ligne de base doit être créée (après quoi le segment sera toujours à jour). Cela est fait automatiquement par le système, mais l&#39;évaluation planifiée (également appelée segmentation programmée) doit d&#39;abord être activée pour que le nettoyage ait lieu.

Avec la segmentation planifiée, votre organisation IMS peut créer un calendrier récurrent pour exécuter automatiquement des tâches d’exportation afin d’évaluer les segments.

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

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le guide [d’utilisation du créateur de](../ui/overview.md)segments.