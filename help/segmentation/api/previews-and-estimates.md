---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Service de segmentation;aperçus;estimations;aperçus et estimations;estimations et aperçus;api;API;
solution: Experience Platform
title: Points de terminaison de l’API d’aperçu et d’estimation
topic-legacy: developer guide
description: Au fur et à mesure que la définition de segment est développée, vous pouvez utiliser les outils d’estimation et de prévisualisation dans Adobe Experience Platform pour afficher des informations de niveau résumé afin de vous assurer que vous isolez l’audience attendue.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: a5cc688357e4750dee73baf3fc9af02a9f2e49e3
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 18%

---

# Aperçus et estimations des points de fin

Au fur et à mesure que vous développez une définition de segment, vous pouvez utiliser les outils d’estimation et de prévisualisation dans Adobe Experience Platform pour afficher des informations de niveau résumé afin de vous assurer que vous isolez l’audience attendue.

* **Les prévisualisations fournissent des listes paginées des profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats avec vos attentes.**

* **** Les estimations fournissent des informations statistiques sur une définition de segment, telles que la taille prévue de l’audience, l’intervalle de confiance et l’écart type d’erreur.

>[!NOTE]
>
>Pour accéder à des mesures similaires liées aux données Real-time Customer Profile, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de noms spécifiques ou l’entrepôt de données Profile dans son ensemble, reportez-vous au guide de point de terminaison [aperçu du profil (aperçu de l’exemple d’état)](../../profile/api/preview-sample-status.md), qui fait partie du guide de développement de l’API Profile.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment les en-têtes requis et la manière de lire des exemples d’appels API.

## Comment sont générées les estimations

Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. Le déclenchement de l’échantillonnage de données dépend de la méthode d’ingestion :

* **Ingestion par lots :**  pour l’ingestion par lots, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre.
* **Ingestion par flux :** pour les processus de données en flux continu, une vérification est effectuée toutes les heures pour déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le décompte.

La taille de l’échantillon de l’analyse dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

>[!NOTE]
>
>L’exécution des estimations prend généralement entre 10 et 15 secondes, en commençant par une estimation approximative et en s’affinant au fur et à mesure de la lecture d’un plus grand nombre d’enregistrements.

## Création d’une nouvelle prévisualisation {#create-preview}

Vous pouvez créer une nouvelle prévisualisation en effectuant une requête POST au point de terminaison `/preview`.

>[!NOTE]
>
>Une tâche d’estimation est automatiquement créée lors de la création d’une tâche de prévisualisation. Ces deux tâches partageront le même identifiant.

**Format d’API**

```http
POST /preview
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `predicateExpression` | L’expression PQL qui servira à effectuer la requête sur les données. |
| `predicateType` | Type de prédicat pour l’expression de requête sous `predicateExpression`. Actuellement, la seule valeur acceptée pour cette propriété est `pql/text`. |
| `predicateModel` | Nom de la classe de schéma [!DNL Experience Data Model] (XDM) sur laquelle les données de profil sont basées. |
| `graphType` | Type de graphique à partir duquel vous souhaitez obtenir la grappe. Les valeurs prises en charge sont `none` (sans combinaison d’identités) et `pdg` (réalise des combinaisons d’identités en fonction de votre graphique d’identités privé). |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) avec les détails de la prévisualisation que vous venez de créer.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Propriété | Description |
| -------- | ----------- |
| `state` | L’état actuel de la tâche de prévisualisation. Lors de sa création initiale, il est à l’état &quot;NEW&quot;. Par la suite, il sera à l’état &quot;RUNNING&quot; jusqu’à ce que le traitement soit terminé, auquel cas il deviendra &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `previewId` | Identifiant de la tâche de prévisualisation à utiliser à des fins de recherche lors de l’affichage d’une estimation ou d’une prévisualisation, comme indiqué dans la section suivante. |

## Récupérer les résultats d’une prévisualisation spécifique {#get-preview}

Vous pouvez récupérer des informations détaillées sur une prévisualisation spécifique en envoyant une requête de GET au point de terminaison `/preview` et en fournissant l’ID de prévisualisation dans le chemin d’accès de la requête.

**Format d&#39;API**

```http
GET /preview/{PREVIEW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{PREVIEW_ID}` | La valeur `previewId` de la prévisualisation que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la prévisualisation spécifiée.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `results` | Liste des identifiants d’entité, ainsi que leurs identités associées. Les liens fournis peuvent être utilisés pour rechercher les entités spécifiées à l’aide du [point d’entrée de l’API d’accès au profil](../../profile/api/entities.md). |

## Récupération des résultats d’une tâche d’estimation spécifique {#get-estimate}

Une fois que vous avez créé une tâche de prévisualisation, vous pouvez utiliser sa balise `previewId` dans le chemin d’une requête de GET vers le point de terminaison `/estimate` pour afficher des informations statistiques sur la définition du segment, y compris la taille prévue de l’audience, l’intervalle de confiance et l’écart-type d’erreur.

**Format d&#39;API**

```http
GET /estimate/{PREVIEW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{PREVIEW_ID}` | Une tâche d’estimation n’est déclenchée que lorsqu’une tâche de prévisualisation est créée et que les deux tâches partagent la même valeur d’identifiant à des fins de recherche. Plus précisément, il s’agit de la valeur `previewId` renvoyée lors de la création de la tâche de prévisualisation. |

**Requête**

La requête suivante récupère les résultats d’une tâche d’estimation spécifique.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des détails concernant la tâche d’estimation.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Tableau d’objets indiquant le nombre de profils dans le segment ventilé par espace de noms d’identité. Le nombre total de profils par espace de noms (additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur à la mesure du nombre de profils, car un profil peut être associé à plusieurs espaces de noms. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel. |
| `state` | L’état actuel de la tâche de prévisualisation. L’état est &quot;EN COURS&quot; jusqu’à ce que le traitement soit terminé, à ce moment-là il devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `_links.preview` | Lorsque la valeur `state` est &quot;RESULT_READY&quot;, ce champ fournit une URL pour afficher l’estimation. |

## Étapes suivantes

Après avoir lu ce guide, vous devriez mieux comprendre comment utiliser les prévisualisations et les estimations à l’aide de l’API Segmentation. Pour savoir comment accéder aux mesures liées à vos données Real-time Customer Profile, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de noms spécifiques ou l’entrepôt de données Profile dans son ensemble, consultez le guide de point de terminaison [Aperçu du profil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
