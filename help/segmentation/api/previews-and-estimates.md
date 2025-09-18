---
solution: Experience Platform
title: Prévisualisations et estimations des points d’entrée de l’API
description: Au fur et à mesure que la définition de segment est développée, vous pouvez utiliser les outils d’estimation et de prévisualisation de Adobe Experience Platform pour afficher des informations de niveau résumé afin de vous assurer que vous isolez l’audience prévue.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: a374d261e3b34b30869f1a9e8486d52f5bd658cb
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 18%

---

# Prévisualisations et points d’entrée d’estimations

Lorsque vous développez une définition de segment, vous pouvez utiliser les outils d’estimation et de prévisualisation de Adobe Experience Platform pour afficher des informations de niveau résumé afin de vous assurer que vous isolez l’audience attendue.

* Les **Aperçus** fournissent des listes paginées de profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats par rapport à vos attentes.

* Les **estimations** fournissent des informations statistiques sur une définition de segment, telles que la taille d’audience prévue, l’intervalle de confiance et l’écart type d’erreur.

>[!NOTE]
>
>Pour accéder à des mesures similaires liées aux données du profil client en temps réel, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de noms spécifiques ou la banque de données de profils dans son ensemble, reportez-vous au guide de point d’entrée [aperçu du profil (aperçu de l’exemple de statut)](../../profile/api/preview-sample-status.md), qui fait partie du guide de développement de l’API Profile.

## Commencer

Les points d’entrée utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

## Comment sont générées les estimations

Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou réduit le nombre total de profils de plus de 3 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. Le déclenchement de l’échantillonnage de données dépend de la méthode d’ingestion :

* **Ingestion par lots :** pour l’ingestion par lots, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil d’augmentation ou de diminution de 3 % est atteint, une tâche est exécutée pour mettre à jour le nombre.
* **Ingestion par flux :** pour les workflows de données par flux, une vérification est effectuée toutes les heures pour déterminer si le seuil d’augmentation ou de diminution de 3 % a été atteint. Si c’est le cas, une tâche est automatiquement déclenchée pour mettre à jour le décompte.

La taille de l’échantillon dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités du magasin de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

>[!NOTE]
>
>Les estimations prennent généralement entre 10 et 15 secondes pour s’exécuter, en commençant par une estimation approximative et en affinant au fur et à mesure que davantage d’enregistrements sont lus.

## Création d’une nouvelle prévisualisation {#create-preview}

Vous pouvez créer une nouvelle prévisualisation en effectuant une requête POST au point d’entrée `/preview`.

>[!NOTE]
>
>Une tâche d’estimation est automatiquement créée lors de la création d’une tâche de prévisualisation. Ces deux tâches partageront le même ID.

**Format d’API**

```http
POST /preview
```

**Requête**

+++ Exemple de requête pour créer un aperçu.

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
| `predicateModel` | Nom de la classe de schéma [!DNL Experience Data Model] (XDM) sur laquelle sont basées les données de profil. |
| `graphType` | Type de graphique à partir duquel vous souhaitez obtenir le cluster. Les valeurs prises en charge sont `none` (n’effectue aucune combinaison d’identités) et `pdg` (effectue une combinaison d’identités en fonction de votre graphique d’identités privé). |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) avec les détails de la prévisualisation que vous venez de créer.

+++ Exemple de réponse lors de la création d’un aperçu.

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
| `state` | L’état actuel de la tâche de prévisualisation. Lors de sa création initiale, il est à l’état « NOUVEAU ». Par la suite, il restera à l’état « RUNNING » jusqu’à ce que le traitement soit terminé, auquel cas il deviendra « RESULT_READY » ou « FAILED ». |
| `previewId` | Identifiant de la tâche de prévisualisation à utiliser à des fins de recherche lors de l’affichage d’une estimation ou d’une prévisualisation, comme indiqué dans la section suivante. |

+++

## Récupérer les résultats d’un aperçu spécifique {#get-preview}

Vous pouvez récupérer des informations détaillées sur un aperçu spécifique en adressant une requête GET au point d’entrée `/preview` et en fournissant l’identifiant d’aperçu dans le chemin de la requête.

**Format d’API**

```http
GET /preview/{PREVIEW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{PREVIEW_ID}` | Valeur `previewId` de l’aperçu que vous souhaitez récupérer. |

**Requête**

+++ Exemple de requête pour récupérer un aperçu.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

+++ Exemple de réponse lors de la récupération d’un aperçu.

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
| `results` | Une liste des identifiants d’entité, ainsi que de leurs identités associées. Les liens fournis peuvent être utilisés pour rechercher les entités spécifiées à l’aide du [ point d’entrée de l’API d’accès aux profils](../../profile/api/entities.md). |

+++

## Récupération des résultats d’une tâche d’estimation spécifique {#get-estimate}

Une fois que vous avez créé une tâche d’aperçu, vous pouvez utiliser son `previewId` dans le chemin d’accès d’une requête GET vers le point d’entrée `/estimate` pour afficher des informations statistiques sur la définition du segment, y compris la taille d’audience prévisionnelle, l’intervalle de confiance et l’écart type d’erreur.

**Format d’API**

```http
GET /estimate/{PREVIEW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{PREVIEW_ID}` | Une tâche d’estimation n’est déclenchée que lorsqu’une tâche de prévisualisation est créée et que les deux tâches partagent la même valeur d’identifiant à des fins de recherche. Plus précisément, il s’agit de la valeur `previewId` renvoyée lors de la création de la tâche de prévisualisation. |

**Requête**

La requête suivante récupère les résultats d’une tâche d’estimation spécifique.

+++ Exemple de requête pour récupérer une tâche d’estimation.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des détails concernant la tâche d’estimation.

+++ Exemple de réponse lors de la récupération d’une tâche d’estimation.

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
| `estimatedNamespaceDistribution` | Tableau d’objets indiquant le nombre de profils dans la définition de segment répartis par espace de noms d’identité. Le nombre total de profils par espace de noms (en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur à la mesure du nombre de profils, car un profil peut être associé à plusieurs espaces de noms. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel. |
| `state` | L’état actuel de la tâche de prévisualisation. L’état est « RUNNING » jusqu’à ce que le traitement soit terminé, auquel cas il devient « RESULT_READY » ou « FAILED ». |
| `_links.preview` | Lorsque l’`state` est « RESULT_READY », ce champ fournit une URL pour afficher l’estimation. |

+++

## Étapes suivantes

Vous êtes arrivé au bout de ce guide. À présent, vous devriez mieux comprendre comment utiliser les aperçus et les estimations à l’aide de l’API Segmentation. Pour savoir comment accéder aux mesures liées à vos données de profil client en temps réel, telles que le nombre total de fragments de profil et de profils fusionnés dans des espaces de noms spécifiques ou la banque de données de profils dans son ensemble, consultez le guide de point d’entrée [aperçu du profil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).
