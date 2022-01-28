---
keywords: Experience Platform;accueil;rubriques populaires;segmentation;Segmentation;Segmentation Service;segmentation Edge;segmentation Edge;segmentation Edge;edge
solution: Experience Platform
title: 'Segmentation Edge à l’aide de l’API '
topic-legacy: developer guide
description: Ce document contient des exemples d’utilisation de la segmentation Edge avec l’API Adobe Experience Platform Segmentation Service.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: e52aa55adde532d838d5417feba36913ed03ce29
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 7%

---

# Segmentation Edge

>[!NOTE]
>
>Le document suivant indique comment effectuer une segmentation Edge à l’aide de l’API. Pour plus d’informations sur l’exécution de la segmentation Edge à l’aide de l’interface utilisateur, veuillez lire le [Guide de l’interface utilisateur de segmentation Edge](../ui/edge-segmentation.md).
>
>La segmentation Edge est désormais disponible en général pour tous les utilisateurs de Platform. Si vous avez créé des segments Edge au cours de la version bêta, ces segments continueront à fonctionner.

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform, ce qui permet d’utiliser les cas de personnalisation de page suivante et de page identique.

>[!IMPORTANT]
>
> Les données Edge seront stockées dans un emplacement de serveur Edge le plus proche de l’emplacement où elles ont été collectées et peuvent être stockées à un autre emplacement que celui désigné comme centre de données Adobe Experience Platform principal (ou hub).
>
> En outre, le moteur de segmentation Edge ne traitera que les demandes sur la périphérie lorsqu’il existe des **one** Identité marquée Principale, qui est cohérente avec les identités Principales non basées sur un bord.

## Prise en main

Ce guide de développement nécessite une compréhension pratique des différentes [!DNL Adobe Experience Platform] services impliqués dans la segmentation Edge. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [[!DNL Segmentation]](../home.md): Permet de créer des segments et des audiences à partir de vos [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Pour passer avec succès des appels à des points de terminaison d’API Experience Platform, veuillez lire le guide sur [Prise en main des API Platform](../../landing/api-guide.md) pour en savoir plus sur les en-têtes requis et sur la lecture d’exemples d’appels API.

## Types de requête de segmentation Edge {#query-types}

Pour qu’un segment soit évalué à l’aide de la segmentation Edge, la requête doit respecter les instructions suivantes :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | Les personnes qui ont ajouté un article à leur panier. |
| Événement unique qui fait référence à un profil | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant sans restriction temporelle. | Des personnes qui vivent aux États-Unis et ont visité la page d&#39;accueil. |
| Événement unique dégradé avec un attribut de profil | Toute définition de segment qui fait référence à un seul événement entrant négatif et à un ou plusieurs attributs de profil | Personnes qui vivent aux Etats-Unis et qui ont **not** a visité la page d’accueil. |
| Événement unique dans une fenêtre de temps de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant dans les 24 heures. | Les personnes qui ont consulté la page d’accueil au cours des dernières 24 heures. |
| Événement unique avec un attribut de profil dans une fenêtre de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Des personnes qui vivent aux États-Unis et ont visité la page d&#39;accueil au cours des dernières 24 heures. |
| Evénement unique dégradé avec un attribut de profil dans une fenêtre de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Personnes qui vivent aux Etats-Unis et qui ont **not** a visité la page d’accueil au cours des dernières 24 heures. |
| Événement de fréquence dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes ayant consulté la page d’accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence avec un attribut de profil dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes des Etats-Unis qui ont visité la page d&#39;accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence associé à un profil dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement négatif qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes qui n’ont pas consulté la page d’accueil **more** plus de cinq fois au cours des dernières 24 heures. |
| Plusieurs accès entrants dans un profil temporel de 24 heures | Toute définition de segment qui fait référence à plusieurs événements qui se produisent dans une fenêtre temporelle de 24 heures. | Personnes ayant consulté la page d’accueil **ou** a consulté la page de passage en caisse au cours des dernières 24 heures. |
| Plusieurs événements avec un profil dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à plusieurs événements se produisant dans une fenêtre temporelle de 24 heures. | Personnes des Etats-Unis qui ont visité la page d&#39;accueil **et** a consulté la page de passage en caisse au cours des dernières 24 heures. |

En outre, le segment **must** être lié à une stratégie de fusion principale. Pour plus d’informations sur les stratégies de fusion, consultez la section [guide des stratégies de fusion](../../profile/api/merge-policies.md).

## Récupération de tous les segments activés pour la segmentation Edge

Vous pouvez récupérer une liste de tous les segments activés pour la segmentation Edge dans votre organisation IMS en envoyant une requête de GET à la fonction `/segment/definitions` point de terminaison .

**Format d&#39;API**

Pour récupérer les segments activés pour la segmentation Edge, vous devez inclure le paramètre de requête . `evaluationInfo.synchronous.enabled=true` dans le chemin d’accès de la requête.

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

Une réponse réussie renvoie un tableau de segments de votre organisation IMS activés pour la segmentation Edge. Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans la section [guide d’entrée des définitions de segment](./segment-definitions.md).

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

Vous pouvez créer un segment activé pour la segmentation Edge en adressant une requête de POST à la fonction `/segment/definitions` point de terminaison qui correspond à l’un des [Types de requête de segmentation Edge répertoriés ci-dessus](#query-types).

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

>[!NOTE]
>
>L’exemple ci-dessous illustre une requête standard pour créer un segment. Pour plus d’informations sur la création d’une définition de segment, consultez le tutoriel sur [création d’un segment](../tutorials/create-a-segment.md).

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

Maintenant que vous savez comment créer des segments activés pour la segmentation Edge, vous pouvez les utiliser pour activer des cas d’utilisation de la personnalisation de la même page et de la page suivante.

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le [guide d’utilisation du créateur de segments](../ui/segment-builder.md).
