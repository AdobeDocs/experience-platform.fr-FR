---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Informations sur l’observabilité de la plate-forme Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# Présentation d’Adobe Experience Platform Observability Insights

Observability Insights est une API RESTful qui vous permet d’exposer les mesures d’observabilité clés dans Adobe Experience Platform. Ces mesures fournissent des informations sur les statistiques d&#39;utilisation des plateformes, les contrôles d&#39;intégrité des services de plateformes, les tendances historiques et les indicateurs de performance pour diverses fonctionnalités de la plate-forme.

Ce document illustre un exemple d’appel à l’API Observability Insights. Pour obtenir une liste complète des points de terminaison de l’Observabilité, consultez la référence [de l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)Observability Insights.

## Prise en main

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les demandes aux API de plateforme requièrent un en-tête qui spécifie le nom du sandbox dans lequel l&#39;opération aura lieu. Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../sandboxes/home.md)sandbox.

* x-sandbox-name : `{SANDBOX_NAME}`

## Récupération des mesures d’observabilité

Vous pouvez récupérer des mesures d’observabilité en faisant une requête GET au point de `/metrics` terminaison dans l’API Observability Insights.

**Format d’API**

Lors de l’utilisation du point de `/metrics` terminaison, au moins un paramètre de demande de mesure doit être fourni. D’autres paramètres de requête sont facultatifs pour le filtrage des résultats.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Paramètre | Description |
| --- | --- |
| `{METRIC}` | Mesure que vous souhaitez exposer. Lorsque vous combinez plusieurs mesures dans un seul appel, vous devez utiliser une esperluette (`&`) pour séparer des mesures individuelles. Par exemple : `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Identifiant d&#39;une ressource de plateforme particulière dont vous souhaitez exposer les mesures. Cet identifiant peut être facultatif, obligatoire ou non, selon les mesures utilisées. Pour obtenir une liste des mesures disponibles, ainsi que les ID pris en charge (obligatoires et facultatifs) pour chaque mesure, reportez-vous au document de référence sur les mesures [](metrics.md)disponibles. |
| `{DATE_RANGE}` | Plage de dates des mesures à exposer, au format ISO 8601 (par exemple `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

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

Une réponse réussie renvoie une liste d’objets, chacun contenant un horodatage dans les valeurs fournies `dateRange` et correspondantes pour les mesures spécifiées dans le chemin de la requête. Si la ressource `id` d&#39;une plateforme est incluse dans le chemin d&#39;accès à la demande, les résultats s&#39;appliquent uniquement à cette ressource particulière. Si le `id` SGI n&#39;est pas utilisé, les résultats s&#39;appliqueront à toutes les ressources applicables au sein de votre organisation.

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

Ce document présente un aperçu de l’API Observability Insights. Consultez le document sur les mesures [](metrics.md) disponibles pour obtenir une liste complète des mesures qui peuvent être utilisées dans l’API.