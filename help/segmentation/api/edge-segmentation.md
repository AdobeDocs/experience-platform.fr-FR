---
solution: Experience Platform
title: Effectuer une segmentation Edge à l’aide de l’API
description: Ce document contient des exemples d’utilisation de la segmentation Edge avec l’API Segmentation Service Adobe Experience Platform.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 89%

---

# Segmentation Edge

>[!NOTE]
>
>Le document suivant indique comment effectuer une segmentation Edge à l’aide de l’API. Pour plus d’informations sur l’exécution de la segmentation Edge à l’aide de l’interface utilisateur, veuillez lire le [guide de l’interface utilisateur de segmentation Edge](../ui/edge-segmentation.md).
>
>La segmentation Edge est désormais généralement disponible pour tous les utilisateurs et utilisatrices de Platform. Si vous avez créé des définitions de segments Edge au cours de la version Beta, ces définitions de segments continueront à fonctionner.

La segmentation Edge permet d’évaluer instantanément les définitions de segment dans Adobe Experience Platform, ce qui permet d’activer les cas d’utilisation de la personnalisation de la même page et de la page suivante.

>[!IMPORTANT]
>
> Les données Edge seront stockées dans l’emplacement de serveur Edge le plus proche de l’emplacement où elles ont été collectées et peuvent être stockées à un autre emplacement que celui désigné comme centre de données Adobe Experience Platform principal (ou hub).
>
> En outre, le moteur de segmentation Edge ne traitera que les requêtes sur le serveur Edge lorsqu’il existe **une** identité marquée principale, qui est cohérente avec les identités principales non basées sur le serveur Edge.

## Prise en main

Ce guide de développement nécessite une connaissance pratique des divers services [!DNL Adobe Experience Platform] impliqués dans la segmentation Edge. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md) : vous permet de créer des audiences à partir de données [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Pour passer avec succès des appels à des points d’entrée d’API Experience Platform, consultez le guide sur la [prise en main des API Platform](../../landing/api-guide.md) pour en savoir plus sur les en-têtes requis et sur la lecture d’exemples d’appels d’API.

## Types de requête de segmentation Edge {#query-types}

Pour qu’un segment soit évalué à l’aide de la segmentation Edge, la requête doit respecter les instructions suivantes :

| Type de requête | Détails | Exemple | Exemple PQL |
| ---------- | ------- | ------- | ----------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | Les personnes qui ont ajouté un article à leur panier. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Profil unique | Toute définition de segment qui fait référence à un seul attribut de profil unique | Personnes qui vivent aux États-Unis. | `homeAddress.countryCode = "US"` |
| Événement unique qui fait référence à un profil | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant sans restriction temporelle. | Personnes qui vivent aux États-Unis et qui ont visité la page d’accueil. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Événement unique annulé avec un attribut de profil | Toute définition de segment qui fait référence à un seul événement entrant annulé et à un ou plusieurs attributs de profil | Personnes qui vivent aux Etats-Unis et qui n’ont **pas** visité la page d’accueil. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Événement unique dans une fenêtre temporelle | Toute définition de segment qui fait référence à un seul événement entrant au cours d’une période donnée. | Personnes qui ont consulté la page d’accueil au cours des dernières 24 heures. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Événement unique avec un attribut de profil dans une fenêtre de temps relatif inférieure à 24 heures | Toute définition de segment qui fait référence à un seul événement entrant, avec un ou plusieurs attributs de profil, et qui se produit dans une fenêtre de temps relative de moins de 24 heures. | Personnes qui vivent aux États-Unis et qui ont visité la page d’accueil au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Événement unique annulé avec un attribut de profil dans une fenêtre temporelle | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant annulé sur une période donnée. | Personnes qui vivent aux États-Unis et qui n’ont **pas** visité la page d’accueil au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| Événement de fréquence dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes ayant consulté la page d’accueil **au moins** cinq fois au cours des dernières 24 heures. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Événement de fréquence avec un attribut de profil dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes originaires des États-Unis qui ont visité la page d’accueil **au moins** cinq fois au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Événement de fréquence associé à un profil dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement annulé qui se produit un certain nombre de fois dans un intervalle de temps de 24 heures. | Personnes qui n’ont pas consulté la page d’accueil **plus** de cinq fois au cours des dernières 24 heures. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Plusieurs accès entrants dans un profil temporel de 24 heures | Toute définition de segment qui fait référence à plusieurs événements qui se produisent dans un intervalle de temps de 24 heures. | Personnes ayant consulté la page d’accueil **ou** ayant consulté la page de passage en caisse au cours des dernières 24 heures. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Plusieurs événements avec un profil dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à plusieurs événements se produisant dans un intervalle de temps de 24 heures. | Personnes originaires des États-Unis qui ont visité la page d’accueil **et** qui ont consulté la page de passage en caisse au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lots ou en diffusion en flux continu. | Personnes qui vivent aux États-Unis et qui se trouvent dans le segment « segment existant ». | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Requête qui fait référence à une carte | Toute définition de segment qui fait référence à une carte de propriétés. | Personnes ayant effectué un ajout à leur panier en fonction de données de segment externes. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

En outre, le segment **doit** être lié à une politique de fusion activée sur le serveur Edge. Pour plus d’informations sur les politiques de fusion, consultez le [guide des politiques de fusion](../../profile/api/merge-policies.md).

Une définition de segment ne sera **pas** activée pour la segmentation Edge dans les scénarios suivants :

- La définition de segment comprend une combinaison d’un événement unique et d’un événement `inSegment`.
   - Toutefois, si le segment contenu dans l’événement `inSegment` est un segment de profil uniquement, la définition de segment **sera** activée pour la segmentation Edge.
- La définition de segment utilise &quot;Ignorer l’année&quot; dans le cadre de ses contraintes temporelles.

## Récupérer tous les segments activés pour la segmentation Edge

Vous pouvez récupérer une liste de tous les segments activés pour la segmentation Edge au sein de votre organisation en envoyant une requête de GET au point de terminaison `/segment/definitions`.

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

Une réponse réussie renvoie un tableau de segments de votre entreprise activés pour la segmentation Edge. Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans le [guide de point d’entrée des définitions de segment](./segment-definitions.md).

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