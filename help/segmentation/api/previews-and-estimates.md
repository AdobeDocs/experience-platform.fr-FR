---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; prévisualisations ; estimations ; prévisualisations et estimations ; estimations et prévisualisations ; api ; API ;
solution: Experience Platform
title: Points de terminaison de l'API prévisualisations et estimations
topic: developer guide
description: Les points de terminaison prévisualisations et estimations de l’API Service de segmentation Adobe Experience Platform vous permettent de vue des informations de niveau récapitulatif afin de vous assurer que vous isolez l’audience attendue dans vos segments.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 26%

---


# Prévisualisations et estimations des points de terminaison

Au fur et à mesure que vous développez votre définition de segment, vous pouvez utiliser les outils d&#39;estimation et de prévisualisation dans [!DNL Adobe Experience Platform] pour vue des informations de synthèse afin de vous assurer que vous isolez l&#39;audience attendue. **Les prévisualisations fournissent des listes paginées des profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats avec vos attentes.** **Les** estimations fournissent des informations statistiques sur une définition de segment, telles que la taille d’audience estimée, l’intervalle de confiance et l’écart-type d’erreur.

## Prise en main

Les points de terminaison utilisés dans ce guide font partie de l&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API, y compris les en-têtes requis et pour savoir comment lire des exemples d&#39;appels d&#39;API.

## Comment sont générées les estimations

La façon dont l’échantillonnage des données est déclenché dépend de la méthode d’assimilation.

Pour l’assimilation par lot, le magasin de profils est automatiquement analysé toutes les quinze minutes afin de déterminer si un nouveau lot a été correctement assimilé depuis l’exécution de la dernière tâche d’échantillonnage. Si tel est le cas, le magasin de profils est ensuite analysé pour voir s&#39;il y a eu au moins 5 % de changement dans le nombre d&#39;enregistrements. Si ces conditions sont remplies, une nouvelle tâche d’échantillonnage est déclenchée.

Pour l’assimilation en flux continu, le magasin de profils est automatiquement analysé toutes les heures afin de déterminer s’il y a eu au moins 5 % de changement dans le nombre d’enregistrements. Si cette condition est remplie, une nouvelle tâche d’échantillonnage est déclenchée.

La taille d’échantillon de l’analyse dépend du nombre total d’entités présentes dans votre magasin de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

>[!NOTE]
>
>Les estimations prennent généralement entre 10 et 15 secondes à s&#39;exécuter, en commençant par une estimation approximative et à être affinées au fur et à mesure que les enregistrements sont lus.

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
| `predicateModel` | Le nom du schéma [!DNL Experience Data Model] (XDM) sur lequel reposent les données du profil. |

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
| `results` | Liste d’identifiants d’entité, ainsi que de leurs identités associées. Les liens fournis peuvent être utilisés pour rechercher les entités spécifiées, à l&#39;aide de [[!DNL Profile Access API]](../../profile/api/entities.md). |

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
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `state` | L’état actuel de la tâche de prévisualisation. Affichera « RUNNING » jusqu’à la fin du traitement, et deviendra alors « RESULT_READY » ou « FAILED ». |
| `_links.preview` | Lorsque l’état actuel de la tâche de prévisualisation affiche « RESULT_READY », cet attribut fournit une URL pour afficher l’estimation. |

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment utiliser les prévisualisations et les estimations. Pour en savoir plus sur les autres [!DNL Segmentation Service] points de terminaison de l&#39;API, consultez le [Guide du développeur du service de segmentation](./overview.md).