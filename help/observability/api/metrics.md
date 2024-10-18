---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API de mesures
description: Découvrez comment récupérer les mesures d’observabilité dans Experience Platform à l’aide de l’API Observability Insights.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: a029d503d37d7e705897ce8efca98674ccf21780
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 25%

---

# Point de terminaison des mesures

Les mesures d’observabilité fournissent des informations sur les statistiques d’utilisation, les tendances historiques et les indicateurs de performances de diverses fonctionnalités de Adobe Experience Platform. Le point d’entrée `/metrics` de [!DNL Observability Insights API] vous permet de récupérer par programmation les données de mesure pour l’activité de votre organisation dans [!DNL Platform].

>[!NOTE]
>
>La version précédente du point de terminaison des mesures (V1) a été abandonnée. Ce document porte exclusivement sur la version actuelle (V2). Pour plus d’informations sur le point de terminaison V1 pour les implémentations héritées, reportez-vous à la [référence d’API](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Récupération des mesures d’observabilité

Vous pouvez récupérer des données de mesure en envoyant une requête de POST au point de terminaison `/metrics`, en spécifiant les mesures que vous souhaitez récupérer dans la payload.

**Format d’API**

```http
POST /metrics
```

**Requête**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `start` | Date/heure la plus ancienne à partir de laquelle récupérer les données de mesure. |
| `end` | Date/heure la plus récente à partir de laquelle récupérer les données de mesure. |
| `granularity` | Champ facultatif qui indique l’intervalle de temps pour lequel diviser les données de mesure. Par exemple, une valeur de `DAY` renvoie des mesures pour chaque jour entre la date `start` et `end`, tandis qu’une valeur de `MONTH` regrouperait les résultats des mesures par mois à la place. |
| `metrics` | Tableau d’objets, un pour chaque mesure que vous souhaitez récupérer. |
| `name` | Nom d’une mesure reconnue par Observability Insights. Consultez l’ [annexe](#available-metrics) pour obtenir la liste complète des noms de mesure acceptés. |
| `filters` | Champ facultatif qui vous permet de filtrer les mesures selon des jeux de données spécifiques. Le champ est un tableau d’objets (un pour chaque filtre), chaque objet contenant les propriétés suivantes : <ul><li>`name` : type d’entité par rapport auquel filtrer les mesures. Actuellement, seul `dataSets` est pris en charge.</li><li>`value` : identifiant d’un ou de plusieurs jeux de données. Plusieurs identifiants de jeu de données peuvent être fournis sous la forme d’une seule chaîne, chaque identifiant étant séparé par des caractères de barre verticale (`\|`).</li><li>`groupBy` : lorsqu’elle est définie sur true, indique que le `value` correspondant représente plusieurs jeux de données dont les résultats de mesure doivent être renvoyés séparément. S’il est défini sur false, les résultats des mesures de ces jeux de données sont regroupés.</li></ul> |
| `aggregator` | Spécifie la fonction d’agrégation qui doit être utilisée pour regrouper plusieurs enregistrements de série temporelle en résultats uniques. Les agrégateurs actuellement pris en charge sont min, max, sum et avg selon la définition de la mesure. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les points de données résultants pour les mesures et les filtres spécifiés dans la requête.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `metricResponses` | Tableau dont les objets représentent chacune des mesures spécifiées dans la requête. Chaque objet contient des informations sur la configuration du filtre et les données de mesure renvoyées. |
| `metric` | Nom de l’une des mesures fournies dans la requête. |
| `filters` | Configuration de filtre pour la mesure spécifiée. |
| `datapoints` | Tableau dont les objets représentent les résultats de la mesure et des filtres spécifiés. Le nombre d’objets dans le tableau dépend des options de filtre fournies dans la requête. Si aucun filtre n’a été fourni, le tableau ne contient qu’un seul objet représentant tous les jeux de données. |
| `groupBy` | Si plusieurs jeux de données ont été spécifiés dans la propriété `filter` pour une mesure et que l’option `groupBy` a été définie sur true dans la requête, cet objet contiendra l’identifiant du jeu de données auquel la propriété `dps` correspondante s’applique.<br><br>Si cet objet apparaît vide dans la réponse, la propriété `dps` correspondante s’applique à tous les jeux de données fournis dans le tableau `filters` (ou à tous les jeux de données de [!DNL Platform] si aucun filtre n’a été fourni). |
| `dps` | Les données renvoyées pour la mesure, le filtre et la période donnés. Chaque clé de cet objet représente un horodatage avec une valeur correspondante pour la mesure spécifiée. La période entre chaque point de données dépend de la valeur `granularity` spécifiée dans la requête. |

{style="table-layout:auto"}

## Annexe

La section suivante contient des informations supplémentaires sur l’utilisation du point de terminaison `/metrics`.

### Mesures disponibles {#available-metrics}

Les tableaux suivants répertorient toutes les mesures exposées par [!DNL Observability Insights], ventilées par service [!DNL Platform]. Chaque mesure comprend une description et un paramètre de requête d’identifiant accepté.

>[!NOTE]
>
>Tous les paramètres de requête d’ID répertoriés sont facultatifs, sauf indication contraire.

#### [!DNL Data Ingestion] {#ingestion}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Data Ingestion]. Les mesures en **gras** sont des mesures d’ingestion par flux.

| Mesure Statistiques | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Taille cumulée de toutes les données ingérées pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.dailysize | Taille des données ingérées quotidiennement pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.batchfailed.count | Nombre de lots échoués pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.batchsuccess.count | Nombre de lots ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.recordsuccess.count | Nombre d’enregistrements ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.presence.count** | Nombre total de messages « présence » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.inlet.total.messages.received** | Nombre total de messages reçus pour un inlet de données ou tous les inlets de données. | ID d’entrée |
| **timeseries.data.collection.inlet.total.messages.size.received** | Taille totale des données reçues pour un inlet de données ou tous les inlets de données. | ID d’entrée |
| **timeseries.data.collection.inlet.success** | Nombre total d’appels HTTP réussis à un inlet de données ou tous les inlets de données. | ID d’entrée |
| **timeseries.data.collection.inlet.failure** | Nombre total d’appels HTTP échoués à un inlet de données ou tous les inlets de données. | ID d’entrée |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Identity Service].

| Mesure Statistiques | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Nombre d’enregistrements écrits dans leur source de données par [!DNL Identity Service] pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.identity.dataset.recordfailed.count | Nombre d’enregistrements échoués par [!DNL Identity Service], pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Nombre d’enregistrements d’identité ignorés. | ID d’organisation |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation pour une force de graphique spécifique (&quot;inconnu&quot;, &quot;faible&quot; ou &quot;fort&quot;). | Force de graphique (**obligatoire**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

Le tableau suivant décrit les mesures pour [!DNL Real-Time Customer Profile].

| Mesure Statistiques | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Nombre d’enregistrements lus de [!DNL Data Lake] par [!DNL Profile] pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.profiles.dataset.recordsuccess.count | Nombre d’enregistrements écrits dans leur source de données par [!DNL Profile], pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.profiles.dataset.batchsuccess.count | Nombre de [!DNL Profile] lots ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |

{style="table-layout:auto"}

### Messages d’erreur

Les réponses du point d’entrée `/metrics` peuvent renvoyer des messages d’erreur dans certaines conditions. Ces messages d’erreur sont renvoyés au format suivant :

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `title` | Chaîne contenant le message d’erreur et la raison potentielle pour laquelle il s’est produit. |
| `report` | Contient des informations contextuelles sur l’erreur, y compris l’environnement de test et l’organisation utilisés dans l’opération qui l’a déclenchée. |

{style="table-layout:auto"}

Le tableau suivant répertorie les différents codes d’erreur qui peuvent être renvoyés par l’API :

| Code d’erreur | Titre | Description |
| --- | --- | --- |
| `INSGHT-1000-400` | Charge utile de requête incorrecte | Un problème s’est produit avec le payload de la requête. Assurez-vous de correspondre exactement à la mise en forme de la payload comme indiqué [au-dessus](#v2). L’une des raisons possibles peut déclencher cette erreur :<ul><li>Champs obligatoires manquants, tels que `aggregator`</li><li>Mesures non valides</li><li>La requête contient un agrégateur non valide</li><li>Une date de début a lieu après une date de fin</li></ul> |
| `INSGHT-1001-400` | Échec de la requête des mesures | Une erreur s’est produite lors de la tentative d’interrogation de la base de données de mesures, en raison d’une mauvaise requête ou de l’impossibilité d’analyser la requête elle-même. Assurez-vous que votre requête est correctement formatée avant de réessayer. |
| `INSGHT-1001-500` | Échec de la requête des mesures | Une erreur s’est produite lors de la tentative d’interrogation de la base de données de mesures, en raison d’une erreur du serveur. Essayez à nouveau la demande. Si le problème persiste, contactez le support Adobe. |
| `INSGHT-1002-500` | Erreur de service | La demande n’a pas pu être traitée en raison d’une erreur interne. Essayez à nouveau la demande. Si le problème persiste, contactez le support Adobe. |
| `INSGHT-1003-401` | Erreur de validation des environnements de test | La requête n’a pas pu être traitée en raison d’une erreur de validation de sandbox. Assurez-vous que le nom d’environnement de test que vous avez fourni dans l’en-tête `x-sandbox-name` représente un environnement de test valide et activé pour votre organisation avant de réessayer la requête. |

{style="table-layout:auto"}
