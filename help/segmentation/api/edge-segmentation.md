---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;service de segmentation;segmentation Edge;segmentation Edge;périphérie en flux continu
solution: Experience Platform
title: 'Segmentation Edge à l’aide de l’API '
topic-legacy: developer guide
description: Ce document contient des exemples d’utilisation de la segmentation Edge avec l’API Adobe Experience Platform Segmentation Service.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 3de00fb9ae5348b129a499cfd81d8db6dbac2d46
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 20%

---

# Segmentation Edge (version bêta)

>[!NOTE]
>
>Le document suivant indique comment effectuer une segmentation Edge à l’aide de l’API. Pour plus d’informations sur l’exécution de la segmentation Edge à l’aide de l’interface utilisateur, consultez le [guide de l’interface utilisateur de la segmentation Edge](../ui/edge-segmentation.md). En outre, la segmentation Edge est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform, ce qui permet d’utiliser les cas de personnalisation de page suivante et de page identique.

## Prise en main

Ce guide de développement nécessite une compréhension pratique des différents services [!DNL Adobe Experience Platform] impliqués dans la segmentation de périphérie. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [[!DNL Segmentation]](../home.md): Permet de créer des segments et des audiences à partir de vos  [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Pour passer avec succès des appels à des points d’entrée d’API [!DNL Data Prep], consultez le guide sur [la prise en main des API Platform](../../landing/api-guide.md) pour en savoir plus sur les en-têtes requis et sur la lecture d’exemples d’appels d’API.

## Types de requête de segmentation Edge {#query-types}

Pour qu’un segment soit évalué à l’aide de la segmentation Edge, la requête doit respecter les instructions suivantes :

| Type de requête | Détails |
| ---------- | ------- |
| Accès entrant | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. |
| Accès entrant qui fait référence à un profil | Toute définition de segment qui fait référence à un seul événement entrant, sans restriction temporelle, et à un ou plusieurs attributs de profil. |
| Requête de fréquence | Toute définition de segment qui fait référence à un événement se produisant au moins un certain nombre de fois. |
| Requête de fréquence faisant référence à un profil | Toute définition de segment qui fait référence à un événement se produisant au moins un certain nombre de fois et qui possède un ou plusieurs attributs de profil. |

{style=&quot;table-layout:auto&quot;}

Les types de requête suivants sont **non** actuellement pris en charge par la segmentation Edge :

| Type de requête | Détails |
| ---------- | ------- |
| Fenêtre de temps relatif | Si une requête fait référence à une fenêtre temporelle, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |
| Négation | Si une requête contient une négation ou un événement `not`, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |
| Événements multiples | Si une requête contient plusieurs événements, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |

{style=&quot;table-layout:auto&quot;}

## Récupération de tous les segments activés pour la segmentation Edge

Vous pouvez récupérer une liste de tous les segments activés pour la segmentation Edge dans votre organisation IMS en envoyant une requête GET au point de terminaison `/segment/definitions` .

**Format d&#39;API**

Pour récupérer les segments activés pour la segmentation Edge, vous devez inclure le paramètre de requête `evaluationInfo.synchronous.enabled=true` dans le chemin de requête.

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

Une réponse réussie renvoie un tableau de segments de votre organisation IMS activés pour la segmentation Edge. Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans le [guide de point de terminaison des définitions de segment](./segment-definitions.md).

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

## Création d’un segment activé pour la segmentation Edge

Vous pouvez créer un segment activé pour la segmentation Edge en envoyant une requête de POST au point de terminaison `/segment/definitions` correspondant à l’un des [types de requête de segmentation Edge répertoriés ci-dessus](#query-types).

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

>[!NOTE]
>
>L’exemple ci-dessous illustre une requête standard pour créer un segment. Pour plus d’informations sur la création d’une définition de segment, consultez le tutoriel sur la [création d’un segment](../tutorials/create-a-segment.md).

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

**Réponse**

Une réponse réussie renvoie les détails de la définition de segment nouvellement créée activée pour la segmentation Edge.

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

Maintenant que vous savez comment créer des segments activés pour la segmentation Edge, vous pouvez les utiliser pour activer des cas d’utilisation de la personnalisation de la même page et de la page suivante.

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le [guide d’utilisation du créateur de segments](../ui/segment-builder.md).
