---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
description: Observability Insights est une API RESTful qui vous permet d’afficher les mesures d’observabilité clés dans Adobe Experience Platform. Ces mesures fournissent des insights sur les statistiques d’utilisation de Platform, les contrôles d’intégrité des services Platform, les tendances historiques et les indicateurs de performance pour diverses fonctionnalités de Platform.
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 76%

---


# Présentation d’Adobe Experience Platform Observability Insights

Observability Insights est une API RESTful qui vous permet d’afficher les mesures d’observabilité clés dans Adobe Experience Platform. These metrics provide insights into [!DNL Platform] usage statistics, health-checks for [!DNL Platform] services, historical trends, and performance indicators for various [!DNL Platform] functionalities.

Ce document présente un exemple d’appel à l’API Observability Insights. Pour une liste complète des points de terminaison d’observabilité, consultez la [référence de l’API Observability Insights](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml).

## Prise en main

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../sandboxes/home.md).

* x-sandbox-name: `{SANDBOX_NAME}`

## Récupération des mesures d’observabilité

Vous pouvez récupérer des mesures d’observabilité en effectuant une requête GET sur le point de terminaison `/metrics` dans l’API Observability Insights.

**Format d’API**

Lors de l’utilisation du point de terminaison `/metrics`, au moins un paramètre de requête de mesure doit être fourni. Les autres paramètres de requête sont facultatifs pour le filtrage des résultats.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Paramètre | Description |
| --- | --- |
| `{METRIC}` | La mesure que vous souhaitez afficher. Lorsque vous combinez plusieurs mesures dans un seul appel, vous devez utiliser une esperluette (`&`) pour les séparer. Par exemple : `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | The identifier for a particular [!DNL Platform] resource whose metrics you want to expose. Cet identifiant peut être facultatif, obligatoire ou non applicable en fonction des mesures utilisées. Pour obtenir une liste des mesures disponibles, ainsi que les identifiants pris en charge (obligatoires et facultatifs) pour chaque mesure, consultez le document de référence sur les [mesures disponibles](metrics.md). |
| `{DATE_RANGE}` | La période des mesures que vous souhaitez afficher, au format ISO 8601 (par exemple, `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets, dont chacun contient une date et heure dans la `dateRange` fournie et les valeurs correspondantes pour les mesures spécifiées dans le chemin de requête. Si l’identifiant `id` d’une ressource de est inclus dans le chemin de requête, les résultats s’appliqueront uniquement à cette ressource particulière. [!DNL Platform] Si l’identifiant `id` est omis, les résultats s’appliqueront à toutes les ressources applicables au sein de votre organisation IMS.

```json
{
    "id": "5cf8ab4ec48aba145214abeb",
    "imsOrgId": "{IMS_ORG}",
    "timeseries": {
        "granularity": "MONTH",
        "items": [
            {
                "timestamp": "2019-06-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1125,
                    "timeseries.ingestion.dataset.size": 32320
                }
            },
            {
                "timestamp": "2019-05-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1003,
                    "timeseries.ingestion.dataset.size": 31409
                }
            },
            {
                "timestamp": "2019-04-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-03-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-02-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 390,
                    "timeseries.ingestion.dataset.size": 16801
                }
            }
        ],
        "_page": null,
        "_links": null
    },
    "stats": {}
}
```

## Étapes suivantes

Ce document présente l’API Observability Insights. Consultez le document sur les [mesures disponibles](metrics.md) pour obtenir une liste complète des mesures qui peuvent être utilisées dans l’API.