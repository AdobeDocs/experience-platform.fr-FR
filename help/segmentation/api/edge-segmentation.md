---
solution: Experience Platform
title: Effectuer une segmentation Edge à l’aide de l’API
description: Ce document contient des exemples d’utilisation de la segmentation Edge avec l’API Segmentation Service Adobe Experience Platform.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 828a586f0264147676da5c43c73d3b3b9d50b9c2
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 70%

---

# Segmentation Edge

>[!NOTE]
>
>Le document suivant indique comment effectuer une segmentation Edge à l’aide de l’API. Pour plus d’informations sur l’exécution de la segmentation Edge à l’aide de l’interface utilisateur, veuillez lire le [guide de l’interface utilisateur de segmentation Edge](../ui/edge-segmentation.md).
>
>La segmentation Edge est désormais généralement disponible pour tous les utilisateurs et utilisatrices de Platform. Si vous avez créé des définitions de segments Edge au cours de la version Beta, ces définitions de segments continueront à fonctionner.

La segmentation Edge permet d’évaluer les définitions de segment dans Adobe Experience Platform instantanément sur le serveur Edge, en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

>[!IMPORTANT]
>
> Les données Edge seront stockées dans l’emplacement de serveur Edge le plus proche de l’emplacement où elles ont été collectées et peuvent être stockées à un autre emplacement que celui désigné comme centre de données Adobe Experience Platform principal (ou hub).
>
> En outre, le moteur de segmentation Edge ne traitera que les requêtes sur le serveur Edge lorsqu’il existe **une** identité marquée principale, qui est cohérente avec les identités principales non basées sur le serveur Edge.

## Prise en main

Ce guide de développement nécessite une connaissance pratique des divers services [!DNL Adobe Experience Platform] impliqués dans la segmentation Edge. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md) : permet de créer des audiences à partir de données [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Pour passer avec succès des appels à des points d’entrée d’API Experience Platform, consultez le guide sur la [prise en main des API Platform](../../landing/api-guide.md) pour en savoir plus sur les en-têtes requis et sur la lecture d’exemples d’appels d’API.

## Types de requête de segmentation Edge {#query-types}

Pour qu’un segment soit évalué à l’aide de la segmentation Edge, la requête doit respecter les instructions suivantes :

| Type de requête | Détails |
| ---------- | ------- |
| Événement unique dans une fenêtre temporelle de moins de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant dans une fenêtre temporelle de moins de 24 heures. |
| Profil uniquement | Toute définition de segment qui ne fait référence qu’à un attribut de profil. |
| Événement unique avec un attribut de profil dans une fenêtre temporelle relative de moins de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant, avec un ou plusieurs attributs de profil, et qui se produit dans une fenêtre temporelle relative de moins de 24 heures. |
| Segment de segments | Toute définition de segment contenant une ou plusieurs définitions de segment par lots ou en flux continu. **Remarque :** si un segment est utilisé avec des définitions de segment **par lot**, la disqualification du profil peut prendre **jusqu’à 24 heures**. Si un segment de segments est utilisé avec des définitions de segment **streaming**, la disqualification du profil se produit en flux continu. |
| Plusieurs événements avec un attribut de profil | Toute définition de segment qui fait référence à plusieurs événements non séquentiels **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. |

En outre, le segment **doit** être lié à une politique de fusion activée sur le serveur Edge. Pour plus d’informations sur les politiques de fusion, consultez le [guide des politiques de fusion](../../profile/api/merge-policies.md).

Une définition de segment ne sera **pas** activée pour la segmentation Edge dans les scénarios suivants :

- La définition de segment comprend une combinaison d’un événement unique et d’un événement `inSegment`.
   - Toutefois, si le segment contenu dans l’événement `inSegment` est un segment de profil uniquement, la définition de segment **sera** activée pour la segmentation Edge.
- La définition de segment utilise « Ignorer l’année » dans le cadre de ses contraintes de temps.

## Récupérer tous les segments activés pour la segmentation Edge

Vous pouvez récupérer une liste de tous les segments activés pour la segmentation Edge au sein de votre organisation en envoyant une requête GET au point d’entrée `/segment/definitions`.

**Format d’API**

Pour récupérer les segments activés pour la segmentation Edge, vous devez inclure le paramètre de requête `evaluationInfo.synchronous.enabled=true` dans le chemin d’accès de la requête.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de segments de votre organisation qui sont activés pour la segmentation Edge. Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans le [guide de point d’entrée des définitions de segment](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

## Créer un segment activé pour la segmentation Edge

Vous pouvez créer un segment activé pour la segmentation Edge en adressant une requête POST au point d’entrée `/segment/definitions` qui correspond à l’un des [types de requête de segmentation Edge répertoriés ci-dessus](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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
    "imsOrgId": "{ORG_ID}",
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

## Annexe

La section suivante répertorie les questions fréquentes sur la segmentation Edge :

### Combien de temps faut-il pour qu’un segment soit disponible sur le réseau Edge ?

La disponibilité d’un segment sur le réseau Edge peut prendre jusqu’à une heure.
