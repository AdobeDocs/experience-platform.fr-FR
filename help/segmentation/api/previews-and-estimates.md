---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; prévisualisations ; estimations ; prévisualisations et estimations ; estimations et prévisualisations ; api ; API ;
solution: Experience Platform
title: Points de terminaison de l'API prévisualisations et estimations
topic-legacy: developer guide
description: Au fur et à mesure que la définition de segment est développée, vous pouvez utiliser les outils d’estimation et de prévisualisation dans Adobe Experience Platform pour vue les informations de synthèse afin de vous assurer que vous isolez l’audience attendue.
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 18%

---

# Prévisualisations et estimations des points de terminaison

Au fur et à mesure que vous développez une définition de segment, vous pouvez utiliser les outils d’estimation et de prévisualisation dans Adobe Experience Platform pour vue des informations de synthèse afin de vous assurer que vous isolez l’audience que vous attendez.

* **Les prévisualisations fournissent des listes paginées des profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats avec vos attentes.**

* **Les** estimations fournissent des informations statistiques sur une définition de segment, telles que la taille d’audience estimée, l’intervalle de confiance et l’écart-type d’erreur.

>[!NOTE]
>
>Pour accéder à des mesures similaires liées aux données du Profil client en temps réel, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de nommage spécifiques ou la banque de données de Profil dans son ensemble, consultez le [guide de point de terminaison prévisualisation de profil (exemple d’état de prévisualisation)](../../profile/api/preview-sample-status.md), qui fait partie du guide de développement d’API de Profil.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de l&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API, y compris les en-têtes requis et pour savoir comment lire des exemples d&#39;appels d&#39;API.

## Comment sont générées les estimations

Lorsque l&#39;ingestion d&#39;enregistrements dans le magasin de Profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d&#39;échantillonnage est déclenchée pour mettre à jour le nombre. La façon dont l’échantillonnage des données est déclenché dépend de la méthode d’assimilation :

* **Importation par lot :** Pour l&#39;assimilation par lot, dans les 15 minutes suivant l&#39;assimilation réussie d&#39;un lot dans le magasin de Profils, si le seuil de 5 % d&#39;augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le décompte.
* **assimilation en flux continu :** Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le décompte.

La taille d’échantillon de l’analyse dépend du nombre total d’entités présentes dans votre magasin de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

>[!NOTE]
>
>L&#39;exécution des estimations prend généralement 10 à 15 secondes, en commençant par une estimation approximative et en les affinant au fur et à mesure que les enregistrements sont lus.

## Création d’une nouvelle prévisualisation {#create-preview}

Vous pouvez créer une nouvelle prévisualisation en effectuant une requête POST au point de terminaison `/preview`.

>[!NOTE]
>
>Une tâche d’estimation est automatiquement créée lorsqu’une tâche de prévisualisation est créée. Ces deux tâches partagent le même ID.

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
        "predicateModel": "_xdm.context.profile"
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `predicateExpression` | L’expression PQL qui servira à effectuer la requête sur les données. |
| `predicateType` | Type de prédicat pour l&#39;expression de requête sous `predicateExpression`. Actuellement, la seule valeur acceptée pour cette propriété est `pql/text`. |
| `predicateModel` | Nom de la classe de schéma [!DNL Experience Data Model] (XDM) sur laquelle reposent les données du profil. |

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
| `state` | L’état actuel de la tâche de prévisualisation. Lors de sa création initiale, il sera à l’état &quot;NOUVEAU&quot;. Par la suite, il sera à l’état &quot;EN COURS&quot; jusqu’à ce que le traitement soit terminé, puis devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `previewId` | ID de la tâche de prévisualisation, à utiliser à des fins de recherche lors de l’affichage d’une estimation ou d’une prévisualisation, comme indiqué dans la section suivante. |

## Récupérer les résultats d&#39;une prévisualisation spécifique {#get-preview}

Vous pouvez récupérer des informations détaillées sur une prévisualisation spécifique en adressant une demande de GET au point de terminaison `/preview` et en indiquant l’identifiant de prévisualisation dans le chemin d’accès de la demande.

**Format d’API**

```http
GET /preview/{PREVIEW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{PREVIEW_ID}` | Valeur `previewId` de la prévisualisation à récupérer. |

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
| `results` | Liste d’identifiants d’entité, ainsi que de leurs identités associées. Les liens fournis peuvent être utilisés pour rechercher les entités spécifiées, à l&#39;aide du [point de terminaison de l&#39;API d&#39;accès au profil](../../profile/api/entities.md). |

## Récupération des résultats d’une tâche d’estimation spécifique {#get-estimate}

Une fois que vous avez créé une tâche de prévisualisation, vous pouvez utiliser `previewId` dans le chemin d&#39;une demande de GET vers le point de terminaison `/estimate` pour obtenir des informations statistiques sur la définition de segment, y compris la taille estimée de l&#39;audience, l&#39;intervalle de fiabilité et l&#39;écart type d&#39;erreur.

**Format d’API**

```http
GET /estimate/{PREVIEW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{PREVIEW_ID}` | Une tâche d’estimation n’est déclenchée que lorsqu’une tâche de prévisualisation est créée et que les deux tâches partagent la même valeur d’ID à des fins de recherche. Plus précisément, il s’agit de la valeur `previewId` renvoyée lors de la création de la tâche de prévisualisation. |

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
| `estimatedNamespaceDistribution` | Tableau d’objets indiquant le nombre de profils dans le segment ventilé par espace de nommage d’identité. Le nombre total de profils par espace de nommage (additionnant les valeurs affichées pour chaque espace de nommage) peut être supérieur à la mesure Nombre de profils, car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel. |
| `state` | L’état actuel de la tâche de prévisualisation. L’état sera &quot;EN COURS&quot; jusqu’à ce que le traitement soit terminé, puis devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `_links.preview` | Si `state` est &quot;RESULT_READY&quot;, ce champ fournit une URL pour vue de l&#39;estimation. |

## Étapes suivantes

Après avoir lu ce guide, vous devez mieux comprendre comment utiliser les prévisualisations et les estimations à l’aide de l’API de segmentation. Pour savoir comment accéder aux mesures liées à vos données de Profil client en temps réel, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de nommage spécifiques ou la banque de données de Profil dans son ensemble, consultez le [guide de la prévisualisation de profil (`/previewsamplestatus`) ](../../profile/api/preview-sample-status.md).
