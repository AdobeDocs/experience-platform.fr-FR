---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation en flux continu
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Evaluer les  en temps réel avec la segmentation en flux continu (bêta)

>[!NOTE] La segmentation en flux continu est une fonctionnalité bêta qui sera disponible sur demande.

La segmentation en flux continu (également connue sous le nom d’évaluation  continue) permet d’évaluer instantanément un client dès qu’un  de arrive dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à Adobe Experience Platform, ce qui signifie que l’appartenance aux segments est maintenue à jour sans exécuter les tâches de segmentation programmée.

![](../images/api/streaming-segment-evaluation.png)

## Prise en main

Ce guide du développeur nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la segmentation en flux continu. Avant de commencer ce didacticiel, veuillez consulter la documentation des services suivants :

- [](../../profile/home.md)du client en temps réel : Fournit un de consommateurs unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Segmentation](../home.md): Permet de créer des segments et de  des  à partir de vos données d’client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels aux API de plateforme.

### Lecture des exemples d’appels d’API

Ce guide du développeur fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

Des en-têtes supplémentaires peuvent être nécessaires pour effectuer des requêtes spécifiques. Les en-têtes corrects s’affichent dans chacun des exemples de ce . Veuillez prêter une attention particulière aux exemples de demandes afin de vous assurer que tous les en-têtes requis sont inclus.

### Types de activés pour la segmentation en flux continu

Le tableau suivant  les différents types de de segmentation et indique s’ils prennent en charge ou non la segmentation en flux continu.

| Type de  | Exemple de  | Segmentation en flux continu prise en charge |
| ---------- | ------------ | --------------------------------- |
| Données démographiques simples | &quot;Donnez-moi toutes les personnes dont l&#39;adresse est au Canada.&quot; | Pris en charge |
|  de la série chronologique | &quot;Donnez-moi toutes les personnes qui ont téléchargé Lightroom.&quot; | Pris en charge |
| Données démographiques et séries chronologiques | &quot;Donnez-moi tous les gens qui vivent au Canada et qui ont passé commande au cours des 30 derniers jours.&quot; | Pris en charge |
| Absence d&#39; | &quot;Donnez-moi tous ceux qui ont abandonné deux chariots distincts dans les deux jours qui suivent.&quot; | Pris en charge |
| Multi-entité | &quot;Donnez-moi toutes les personnes dont le type de droits est &quot;Expérimentées&quot;.&quot; | Non pris en charge |
| Fonctions PQL avancées | &quot;Donnez-moi tous les  qui ont passé une commande la semaine dernière, et incluez le SKU et le nom de tous les produits achetés.&quot; | Non pris en charge |

## Récupérer tous les segments de segmentation en flux continu activés

Avant de créer un segment compatible avec la diffusion en continu ou de mettre à jour un segment existant pour qu’il soit compatible avec la diffusion en continu, veillez à ne pas dupliquer les informations en récupérant un  de tous les segments compatibles avec la diffusion en continu.

**Format API**

Pour récupérer les segments activés pour la diffusion en continu, vous devez inclure le paramètre  `evaluationInfo.continuous.enabled=true` dans le chemin de requête.

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

Une fois que vous avez confirmé que le segment que vous souhaitez créer n’existe pas déjà, vous pouvez créer un nouveau segment qui est activé pour la segmentation en flux continu.

**Format API**

```http
POST /segment/definitions
```

**Requête**

La requête suivante crée un segment dont la segmentation en flux continu est activée. Note that the `continuous` section is set to `enabled: true`.

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

>[!NOTE] Il s’agit d’une requête standard &quot;créer un segment&quot;, avec le paramètre ajouté de la `continuous` section défini sur `enabled: true`. Pour plus d’informations sur la création d’une définition de segment, consultez la documentation sur la création [de](../tutorials/create-a-segment.md)segment.

**Réponse**

Une réponse réussie renvoie les détails de la définition de segment en flux continu nouvellement créée.

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

## Activer un segment existant pour la segmentation en flux continu

Vous pouvez activer un segment existant pour la segmentation en flux continu en fournissant l’ID de la définition de segment dans le chemin d’une requête PATCH. En outre, la charge utile de cette requête PATCH doit inclure tous les détails de la définition de segment existante, accessible en adressant une requête GET à la définition de segment en question.

### Recherche d’une définition de segment existante

Pour rechercher une définition de segment existante, vous devez indiquer son ID dans le chemin d’une requête GET.

**Format API**

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

Maintenant que vous connaissez les détails du segment que vous souhaitez mettre à jour, vous pouvez effectuer une requête PATCH pour mettre à jour le segment afin d’activer la segmentation en flux continu.

**Format API**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Requête**

La charge utile de la requête suivante fournit les détails de la définition de segment (obtenue à l’étape [](#look-up-an-existing-segment-definition)précédente) et la met à jour en modifiant sa `continuous.enabled` propriété en `true`.

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

Une réponse réussie renvoie les détails de la définition de segment nouvellement mise à jour.

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

Une fois l’évaluation de diffusion en continu activée, une ligne de base doit être créée (après quoi le segment sera toujours à jour). Cela est fait automatiquement par le système, mais l&#39;évaluation planifiée (également connue sous le nom de segmentation programmée) doit d&#39;abord être activée pour que le nettoyage ait lieu.

Avec la segmentation programmée, votre organisation IMS peut créer un calendrier récurrent pour exécuter automatiquement les tâches d’exportation afin d’évaluer les segments.

>[!NOTE] L’évaluation planifiée peut être activée pour les sandbox avec un maximum de cinq (5) stratégies de fusion pour les  individuels XDM. Si votre entreprise dispose de plus de cinq stratégies de fusion pour XDM Individuel  dans un seul de sandbox , vous ne pourrez pas utiliser l’évaluation planifiée.

### Création d’une planification

En envoyant une requête POST au `/config/schedules` point de fin, vous pouvez créer un calendrier et inclure l’heure spécifique à laquelle le calendrier doit être déclenché.

**Format API**

```http
POST /config/schedules
```

**Requête**

La requête suivante crée un nouveau calendrier en fonction des spécifications fournies dans la charge utile.

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
| `schedule` | **(Obligatoire)** Chaîne contenant la planification de la tâche. Les tâches ne peuvent être planifiées qu’une fois par jour, ce qui signifie que vous ne pouvez pas programmer l’exécution de plusieurs tâches au cours d’une période de 24 heures. L’exemple illustré (`0 0 1 * * ?`) signifie que la tâche est déclenchée tous les jours à 1:00:00 UTC. Pour plus d&#39;informations, veuillez consulter la documentation sur le format [du ](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron . |
| `state` | *(Facultatif)* Chaîne contenant l’état de planification. Valeurs disponibles : `active` et `inactive`. La valeur par défaut est `inactive`. Une organisation IMS ne peut créer qu&#39;une seule planification. Les étapes de mise à jour du calendrier sont disponibles plus loin dans ce didacticiel. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau calendrier créé.

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

Par défaut, une planification est inactive lors de la création, sauf si la `state` propriété est définie sur `active` dans le corps de la requête de création (POST). Vous pouvez activer une planification (définissez la `state` valeur sur `active`) en exécutant une requête PATCH sur le point de fin `/config/schedules` et en incluant l’ID de la planification dans le chemin d’accès.

**Format API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Requête**

La requête suivante utilise le formatage [de correctif](http://jsonpatch.com/) JSON pour mettre à jour `state` le calendrier vers `active`.

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

Maintenant que vous avez activé les segments nouveaux et existants pour la segmentation en flux continu et que vous avez activé la segmentation programmée pour développer une ligne de base et effectuer des évaluations périodiques, vous pouvez commencer à créer des segments pour votre entreprise.

Pour savoir comment exécuter des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le guide [d’utilisation du créateur de](../ui/overview.md)segments.