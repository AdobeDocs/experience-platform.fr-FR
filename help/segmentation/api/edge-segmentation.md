---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; segmentation des contours ; Segmentation des contours ; Segmentation des contours ; Diffusion des contours ;
solution: Experience Platform
title: 'Segmentation des contours à l’aide de l’API '
topic-legacy: developer guide
description: Ce document contient des exemples d’utilisation de la segmentation des contours avec l’API Adobe Experience Platform Segmentation Service.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: c89971668839555347e9b84c7c0a4ff54a394c1a
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 9%

---

# Segmentation des contours (bêta)

>[!NOTE]
>
>Le document suivant indique comment effectuer la segmentation des contours à l’aide de l’API. Pour plus d’informations sur la segmentation des contours à l’aide de l’interface utilisateur, consultez la section [guide de l’interface utilisateur de segmentation des contours](../ui/edge-segmentation.md). En outre, la segmentation des contours est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation Edge permet d’évaluer instantanément les segments de Adobe Experience Platform sur le bord, ce qui permet d’utiliser des cas d’utilisation de personnalisation de la même page et de la page suivante.

## Prise en main

Ce guide du développeur nécessite une compréhension pratique des différents [!DNL Adobe Experience Platform] services impliqués dans la segmentation des contours. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [[!DNL Segmentation]](../home.md): Permet de créer des segments et des publics à partir de votre [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Pour réussir à appeler des points de terminaison API Experience Platform, lisez le guide sur [prise en main des API de plate-forme](../../landing/api-guide.md) pour en savoir plus sur les en-têtes requis et comment lire des exemples d’appels d’API.

## Types de requête de segmentation de contour {#query-types}

Pour qu&#39;un segment soit évalué à l&#39;aide de la segmentation des contours, la requête doit respecter les directives suivantes :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un événement entrant unique sans limitation de temps. | Les personnes qui ont ajouté un article à leur panier. |
| Événement unique faisant référence à un profil | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant sans restriction de temps. | Des gens qui vivent aux États-Unis et ont visité la page d&#39;accueil. |
| Événement unique négatif avec un attribut de profil | Toute définition de segment faisant référence à un événement entrant unique et à un ou plusieurs attributs de profil négatifs | Personnes vivant aux États-Unis et ayant **non** a visité la page d&#39;accueil. |
| Événement unique dans une période de 24 heures | Toute définition de segment faisant référence à un événement entrant unique dans les 24 heures. | Les personnes qui ont visité la page d&#39;accueil ces dernières 24 heures. |
| Événement unique avec un attribut de profil dans une fenêtre de temps de 24 heures | Toute définition de segment faisant référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Des gens qui vivent aux États-Unis et ont visité la page d&#39;accueil ces dernières 24 heures. |
| Événement unique négatif avec un attribut de profil dans une période de 24 heures | Toute définition de segment faisant référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Personnes vivant aux États-Unis et ayant **non** a visité la page d&#39;accueil au cours des dernières 24 heures. |
| Événement de fréquence dans une période de 24 heures | Toute définition de segment qui fait référence à un événement qui se produit un certain nombre de fois dans une période de 24 heures. | Personnes ayant visité la page d&#39;accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence avec un attribut de profil dans une période de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement qui se produit un certain nombre de fois dans une période de 24 heures. | Personnes des États-Unis qui ont visité la page d&#39;accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence négatif avec un profil dans une période de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement annulé qui se produit un certain nombre de fois dans une période de 24 heures. | Personnes qui n&#39;ont pas visité la page d&#39;accueil **plus** plus de cinq fois au cours des dernières 24 heures. |
| Plusieurs visites entrantes dans un profil temporel de 24 heures | Toute définition de segment qui fait référence à plusieurs événements qui se produisent dans une période de 24 heures. | Personnes ayant visité la page d&#39;accueil **ou** a visité la page de paiement au cours des dernières 24 heures. |
| Plusieurs événements avec un profil dans une période de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et plusieurs événements se produisant dans une période de 24 heures. | Des gens des États-Unis qui ont visité la page d&#39;accueil **et** a visité la page de paiement au cours des dernières 24 heures. |

{style=&quot;table-layout:auto&quot;}

## Récupérer tous les segments activés pour la segmentation des contours

Vous pouvez récupérer une liste de tous les segments qui sont activés pour la segmentation des contours au sein de votre organisation IMS en adressant une demande de GET à l’adresse suivante : `/segment/definitions` point de terminaison.

**Format d&#39;API**

Pour récupérer les segments activés pour la segmentation des contours, vous devez inclure le paramètre de requête `evaluationInfo.synchronous.enabled=true` dans le chemin d’accès de la demande.

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

Une réponse réussie renvoie un tableau de segments de votre organisation IMS qui sont activés pour la segmentation des contours. Des informations plus détaillées sur la définition de segment renvoyée sont disponibles dans le fichier [guide d&#39;extrémité des définitions de segment](./segment-definitions.md).

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

## Création d’un segment activé pour la segmentation des contours

Vous pouvez créer un segment qui est activé pour la segmentation des contours en adressant une demande de POST à la `/segment/definitions` point de terminaison correspondant à l’un des [types de requête de segmentation de bord répertoriés ci-dessus](#query-types).

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

>[!NOTE]
>
>L’exemple ci-dessous est une demande standard de création d’un segment. Pour plus d’informations sur la création d’une définition de segment, consultez le tutoriel sur [création d’un segment](../tutorials/create-a-segment.md).

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

Une réponse réussie renvoie les détails de la nouvelle définition de segment qui est activée pour la segmentation des contours.

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
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
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

Maintenant que vous savez comment créer des segments prenant en charge la segmentation des contours, vous pouvez les utiliser pour activer les cas d’utilisation de personnalisation de la même page et de la page suivante.

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le [guide d’utilisation du créateur de segments](../ui/segment-builder.md).
