---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; segmentation des arêtes ; Segmentation des arêtes ; Segmentation des arêtes ; arête de diffusion ;
solution: Experience Platform
title: 'Segmentation Edge à l’aide de l’API '
topic: guide du développeur
description: Ce document contient des exemples d’utilisation de la segmentation des arêtes avec l’API Adobe Experience Platform Segmentation Service.
translation-type: tm+mt
source-git-commit: 0c4625ec0728c8c94b72e3e16e7ecf45ea2d0c0b
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 12%

---


# Segmentation Edge

>[!NOTE]
>
>Le document suivant indique comment effectuer la segmentation des arêtes à l’aide de l’API. Pour plus d&#39;informations sur la segmentation des arêtes à l&#39;aide de l&#39;interface utilisateur, consultez le [guide de l&#39;interface utilisateur de la segmentation des arêtes](../ui/edge-segmentation.md).

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform en périphérie, ce qui permet d’utiliser les mêmes cas de personnalisation de page et de page suivante.

## Prise en main

Ce guide du développeur nécessite une bonne compréhension des différents services [!DNL Adobe Experience Platform] impliqués dans la segmentation des arêtes. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [[!DNL Segmentation]](../home.md): Permet de créer des segments et des audiences à partir de vos  [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Pour réussir à appeler les points de terminaison de l&#39;API [!DNL Data Prep], consultez le guide [prise en main des API de plateforme](../../landing/api-guide.md) pour en savoir plus sur les en-têtes requis et sur la manière de lire les exemples d&#39;appels d&#39;API.

## Types de requête de segmentation Edge {#query-types}

Pour qu’un segment soit évalué à l’aide de la segmentation Edge, la requête doit respecter les consignes suivantes :

| Type de requête | Détails |
| ---------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. |
| Requête de fréquence | Toute définition de segment faisant référence à un événement survenant un certain nombre de fois. |
| Requête de fréquence faisant référence à un profil | Toute définition de segment faisant référence à un événement survenant un certain nombre de fois et ayant un ou plusieurs attributs de profil. |

{style=&quot;table-layout:auto&quot;}

Les types de requête suivants sont **non** actuellement pris en charge par la segmentation des arêtes :

| Type de requête | Détails |
| ---------- | ------- |
| Fenêtre relative | Si une requête fait référence à une fenêtre temporelle, elle ne peut pas être évaluée à l’aide de la segmentation des arêtes. |
| Négation | Si une requête contient une négation ou un événement `not`, elle ne peut pas être évaluée à l’aide de la segmentation des arêtes. |
| Plusieurs événements | Si une requête contient plusieurs événements, elle ne peut pas être évaluée à l’aide de la segmentation des arêtes. |

{style=&quot;table-layout:auto&quot;}

## Récupérer tous les segments activés pour la segmentation des arêtes

Vous pouvez récupérer une liste de tous les segments activés pour la segmentation des arêtes au sein de votre organisation IMS en adressant une demande de GET au point de terminaison `/segment/definitions`.

**Format d’API**

Pour récupérer les segments activés pour la segmentation des arêtes, vous devez inclure le paramètre de requête `evaluationInfo.synchronous.enabled=true` dans le chemin d’accès de la requête.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de segments de votre organisation IMS qui sont activés pour la segmentation des arêtes. Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans le [guide de point de terminaison des définitions de segment](./segment-definitions.md).

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
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

## Créer un segment activé pour la segmentation des arêtes

Vous pouvez créer un segment activé pour la segmentation des arêtes en envoyant une requête de POST au point de terminaison `/segment/definitions`. Outre la correspondance avec l’un des types de requête de segmentation [edge répertoriés ci-dessus](#query-types), vous devez définir l’indicateur `evaluationInfo.synchronous.enabled` dans la charge utile sur true.

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

>[!NOTE]
>
>L’exemple ci-dessous représente une requête standard pour créer un segment. Pour plus d&#39;informations sur la création d&#39;une définition de segment, consultez le didacticiel [Création d&#39;un segment](../tutorials/create-a-segment.md).

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
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | L&#39;objet `evaluationInfo` détermine le type d&#39;évaluation que la définition de segment va subir. Pour utiliser la segmentation des arêtes, définissez `evaluationInfo.synchronous.enabled` sur la valeur `true`. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle définition de segment qui est activée pour la segmentation de périphérie.

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
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Étapes suivantes

Maintenant que vous savez comment créer des segments prenant en charge la segmentation à la périphérie, vous pouvez les utiliser pour activer les cas d’utilisation de la personnalisation de la même page et de la page suivante.

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le [guide d’utilisation du créateur de segments](../ui/segment-builder.md).