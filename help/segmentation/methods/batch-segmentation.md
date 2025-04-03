---
title: Guide de segmentation par lots
description: Découvrez la segmentation par lots, notamment en quoi elle consiste, comment créer une audience évaluée à l’aide de la segmentation par lots et comment afficher vos audiences créées à l’aide de la segmentation par lots.
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 10%

---

# Guide de segmentation par lots

La segmentation par lots est une méthode d’évaluation de segmentation qui vous permet de déplacer les données de profil en même temps pour créer des audiences correspondantes.

La segmentation par lots vous permet de créer des audiences riches et détaillées et d’exécuter des tâches de segmentation afin de déterminer à quel moment vous souhaitez que ces données soient propagées vers les services en aval.

## Types de requête éligibles {#query-types}

Toutes les requêtes sont éligibles à la segmentation par lots.

## Créer une audience {#create-audience}

Vous pouvez créer une audience évaluée à l’aide de la segmentation par lots à l’aide de l’API Segmentation Service ou d’Audience Portal dans l’interface utilisateur.

>[!BEGINTABS]

>[!TAB API Segmentation Service]

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

+++ Exemple de requête pour créer une définition de segment activée pour la segmentation par lots

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de créer.

+++Exemple de réponse lors de la création d’une définition de segment.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Vous trouverez plus d’informations sur l’utilisation de ce point d’entrée dans le [guide de point d’entrée de définition de segment](../api/segment-definitions.md).

>[!TAB Audience Portal]

Dans Audience Portal, sélectionnez **[!UICONTROL Créer une audience]**.

![Le bouton Créer une audience est mis en surbrillance dans le portail d’audiences.](../images/methods/batch/select-create-audience.png)

Une fenêtre contextuelle s’affiche. Sélectionnez **[!UICONTROL Créer des règles]** pour accéder au créateur de segments.

![Le bouton Créer des règles est mis en surbrillance dans la fenêtre contextuelle de création d’audience.](../images/methods/batch/select-build-rules.png)

Après avoir créé votre définition de segment, sélectionnez **[!UICONTROL Lot]** comme **[!UICONTROL Méthode d’évaluation]**.

![La définition de segment s’affiche. Le type d’évaluation est mis en surbrillance, montrant que la définition de segment peut être évaluée à l’aide de la segmentation en flux continu.](../images/methods/batch/batch-evaluation-method.png)

Pour en savoir plus sur la création de définitions de segment, consultez le [guide du créateur de segments](../ui/segment-builder.md)

>[!ENDTABS]

## Récupérer des audiences {#retrieve-audiences}

Vous pouvez récupérer toutes les audiences évaluées à l’aide de la segmentation par lots à l’aide de l’API Segmentation Service ou via Audience Portal dans l’interface utilisateur.

>[!BEGINTABS]

>[!TAB API Segmentation Service]

Récupérez une liste de toutes les définitions de segment évaluées à l’aide de la segmentation par lots au sein de votre organisation en envoyant une requête GET au point d’entrée `/segment/definitions`.

**Format d’API**

Vous devez inclure le paramètre de requête `evaluationInfo.batch.enabled=true` dans le chemin d’accès de la requête pour récupérer les définitions de segment évaluées à l’aide de la segmentation par lots.

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**Requête**

+++ Exemple de requête pour répertorier toutes les définitions de segment activées par lots

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec un tableau de définitions de segment dans votre organisation qui sont évaluées à l’aide de la segmentation par lots.

+++Exemple de réponse contenant une liste de toutes les définitions de segment évaluées par segmentation par lots de votre organisation

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
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
            "imsOrgId": "{ORG_ID}",
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

Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans le [guide de point d’entrée des définitions de segment](../api/segment-definitions.md).

+++

>[!TAB Audience Portal]

Vous pouvez récupérer toutes les audiences activées pour la segmentation par lots au sein de votre organisation en utilisant les filtres d’Audience Portal. Sélectionnez l’icône ![icône de filtre](../../images/icons/filter.png) pour afficher la liste des filtres.

![L’icône de filtre est mise en surbrillance dans Audience Portal.](../images/methods/filter-audiences.png)

Dans les filtres disponibles, accédez à **[!UICONTROL Fréquence des mises à jour]** et sélectionnez « [!UICONTROL Lot] ». L’utilisation de ce filtre affiche toutes les audiences de votre organisation qui sont évaluées à l’aide de la segmentation par lots.

![La fréquence de mise à jour par lots est sélectionnée, affichant toutes les audiences de l’organisation qui sont évaluées à l’aide de la segmentation par lots.](../images/methods/batch/filter-batch.png)

Pour en savoir plus sur l’affichage des audiences dans Experience Platform, consultez le guide [Audience Portal](../ui/audience-portal.md).

>[!ENDTABS]

## Étapes suivantes

Ce guide explique comment créer une définition de segment qui peut être évaluée à l’aide de la segmentation par lots sur Adobe Experience Platform.

Pour en savoir plus sur l’utilisation de l’interface utilisateur d’Experience Platform, veuillez lire le [Guide d’utilisation de la segmentation](../ui/overview.md).

Pour les questions fréquentes sur la segmentation par lots, veuillez lire la section [segmentation par lots](../faq.md#batch-segmentation) de la FAQ.
