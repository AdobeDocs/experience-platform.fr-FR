---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c

---


# Présentation d’Adobe Experience Platform Observability Insights

Observability Insights est une API RESTful qui vous permet d’exposer les mesures d’observabilité clés dans Adobe Experience Platform. Ces mesures fournissent des informations sur les statistiques d’utilisation de la Plateforme, les contrôles d’intégrité des services de la Plateforme, les tendances historiques et les indicateurs de performance pour diverses fonctionnalités de la Plateforme.

Ce montre un exemple d&#39;appel à l&#39;API Observability Insights. Pour un  complet des points de fin d’Observability, reportez-vous à la référence [de l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)Observability Insights.

## Prise en main

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu. Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../sandboxes/home.md)sandbox.

* x-sandbox-name : `{SANDBOX_NAME}`

## Récupérer les mesures d&#39;observabilité

Vous pouvez récupérer des mesures d’observabilité en exécutant une requête GET vers le `/metrics` point de terminaison dans l’API Observability Insights.

**Format API**

Lors de l’utilisation du `/metrics` point de fin, au moins un paramètre de demande de mesure doit être fourni. D’autres paramètres de  sont facultatifs pour le filtrage des résultats.

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
| `{ID}` | Identifiant d’une ressource de plateforme particulière dont vous souhaitez exposer les mesures. Cet identifiant peut être facultatif, obligatoire ou non, selon les mesures utilisées. Pour obtenir un  des mesures disponibles, ainsi que les ID pris en charge (obligatoires et facultatifs) pour chaque mesure, reportez-vous au de référence sur les mesures [](metrics.md)disponibles. |
| `{DATE_RANGE}` | Plage de dates des mesures à exposer, au format ISO 8601 (par exemple, `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

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

Une réponse réussie renvoie un  d’objets, chacun contenant un horodatage dans les valeurs fournies `dateRange` et correspondantes pour les mesures spécifiées dans le chemin de requête. Si une ressource `id` de plateforme est incluse dans le chemin d’accès à la requête, les résultats s’appliqueront uniquement à cette ressource particulière. Si la `id` question n&#39;est pas traitée, les résultats s&#39;appliqueront à toutes les ressources applicables au sein de votre organisation IMS.

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

Ce présente un aperçu de l’API Observability Insights. Consultez le  sur les mesures [](metrics.md) disponibles pour obtenir un complet de mesures pouvant être utilisées dans l’API.