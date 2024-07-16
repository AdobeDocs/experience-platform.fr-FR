---
solution: Experience Platform
title: Points de terminaison de l’API d’aperçu et d’estimation
description: Au fur et à mesure que la définition de segment est développée, vous pouvez utiliser les outils d’estimation et de prévisualisation dans Adobe Experience Platform pour afficher des informations de niveau résumé afin de vous assurer que vous isolez l’audience attendue.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 19%

---

# Aperçus et estimations des points de fin

Au fur et à mesure que vous développez une définition de segment, vous pouvez utiliser les outils d’estimation et de prévisualisation dans Adobe Experience Platform pour afficher des informations de niveau résumé afin de vous assurer que vous isolez l’audience attendue.

* **Les aperçus** fournissent des listes paginées de profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats à ce que vous attendez.

* Les **estimations** fournissent des informations statistiques sur une définition de segment, telles que la taille prévue de l’audience, l’intervalle de confiance et l’écart type d’erreur.

>[!NOTE]
>
>Pour accéder à des mesures similaires liées aux données de Real-Time Customer Profile, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de noms spécifiques ou l’entrepôt de données Profile dans son ensemble, reportez-vous au [guide de point de terminaison d’aperçu de profil (aperçu de l’exemple d’état)](../../profile/api/preview-sample-status.md), partie du guide de développement de l’API Profile.

## Commencer

Les points de terminaison utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et comment lire des exemples d’appels API.

## Comment sont générées les estimations

Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. Le déclenchement de l’échantillonnage de données dépend de la méthode d’ingestion :

* **Ingestion par lots :** Pour l’ingestion par lots, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre.
* **Ingestion par flux :** Pour les flux de données en flux continu, une vérification est effectuée toutes les heures pour déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le décompte.

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

Vous pouvez créer une nouvelle prévisualisation en effectuant une requête POST au point d’entrée `/preview`.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `graphType` | Type de graphique à partir duquel vous souhaitez obtenir la grappe. Les valeurs prises en charge sont `none` (aucune combinaison d’identités) et `pdg` (réalise des combinaisons d’identités basées sur votre graphique d’identités privé). |

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

## Récupération des résultats d’une prévisualisation spécifique {#get-preview}

Vous pouvez récupérer des informations détaillées sur une prévisualisation spécifique en envoyant une requête de GET au point de terminaison `/preview` et en fournissant l’ID de prévisualisation dans le chemin d’accès de la requête.

**Format d’API**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `results` | Liste des identifiants d’entité, ainsi que leurs identités associées. Les liens fournis peuvent être utilisés pour rechercher les entités spécifiées, à l’aide du [point d’entrée de l’API d’accès au profil](../../profile/api/entities.md). |

## Récupération des résultats d’une tâche d’estimation spécifique {#get-estimate}

Une fois que vous avez créé une tâche de prévisualisation, vous pouvez utiliser son `previewId` dans le chemin d’une requête de GET vers le point de terminaison `/estimate` pour afficher des informations statistiques sur la définition de segment, y compris la taille prévue de l’audience, l’intervalle de confiance et l’écart type d’erreur.

**Format d’API**

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_links.preview` | Lorsque `state` est &quot;RESULT_READY&quot;, ce champ fournit une URL pour afficher l’estimation. |

## Étapes suivantes

Après avoir lu ce guide, vous devriez mieux comprendre comment utiliser les prévisualisations et les estimations à l’aide de l’API Segmentation. Pour savoir comment accéder aux mesures liées à vos données de profil client en temps réel, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de noms spécifiques ou l’entrepôt de données de profil dans son ensemble, consultez le [guide de point de terminaison de prévisualisation de profil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
