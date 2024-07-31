---
keywords: Experience Platform;accueil;rubriques les plus consultées;flow service;
title: Création d’une exécution de flux pour l’ingestion à la demande à l’aide de l’API Flow Service
description: Découvrez comment créer une exécution de flux pour l’ingestion à la demande à l’aide de l’API Flow Service
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 13%

---

# Créez une exécution de flux pour l’ingestion à la demande à l’aide de l’API [!DNL Flow Service].

Les exécutions de flux représentent une instance d’exécution de flux. Par exemple, si un flux est planifié pour s’exécuter toutes les heures à 9 h, 10 h et 11 h, il y a trois instances d’un flux. Les exécutions de flux sont spécifiques à votre organisation.

L’ingestion à la demande vous permet de créer un flux exécuté sur un flux donné. Cela permet à vos utilisateurs de créer une exécution de flux, en fonction de paramètres donnés, et de créer un cycle d’ingestion, sans jetons de service. La prise en charge de l’ingestion sur demande est disponible uniquement pour les sources par lots.

Ce tutoriel décrit les étapes à suivre pour utiliser l’ingestion à la demande et créer une exécution de flux à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Commencer

>[!NOTE]
>
>Pour créer une exécution de flux, vous devez d’abord disposer de l’identifiant de flux d’un flux de données planifié pour une ingestion unique.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Création d’une exécution de flux pour une source basée sur un tableau

Pour créer un flux pour une source basée sur une table, envoyez une requête de POST à l’API [!DNL Flow Service] tout en fournissant l’identifiant du flux sur lequel vous souhaitez créer l’exécution, ainsi que les valeurs des colonnes heure de début, heure de fin et delta.

>[!TIP]
>
>Les sources basées sur un tableau comprennent les catégories de sources suivantes : publicité, analyse, consentement et préférences, CRM, succès client, base de données, automatisation du marketing, paiements et protocoles.

**Format d’API**

```http
POST /runs/
```

**Requête**

La requête suivante crée une exécution de flux pour l’ID de flux `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Il vous suffit de fournir le `deltaColumn` lors de la création de votre première exécution de flux. Après cela, `deltaColumn` sera corrigé dans le cadre de la transformation `copy` du flux et sera traité comme la source de vérité. Toute tentative de modification de la valeur `deltaColumn` via les paramètres d’exécution de flux entraînera une erreur.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `flowId` | L’identifiant du flux sur lequel votre exécution de flux sera créée. |
| `params.startTime` | Heure planifiée du début de l’exécution du flux à la demande. Cette valeur est représentée en heure unique. |
| `params.windowStartTime` | Date et heure de récupération des données au plus tôt. Cette valeur est représentée en heure unique. |
| `params.windowEndTime` | Date et heure auxquelles les données seront récupérées. Cette valeur est représentée en heure unique. |
| `params.deltaColumn` | La colonne delta est nécessaire pour partitionner les données et séparer les données nouvellement ingérées des données historiques. **Remarque** : `deltaColumn` n’est nécessaire que lors de la création de votre première exécution de flux. |
| `params.deltaColumn.name` | Nom de la colonne delta. |

**Réponse**

Une réponse réussie renvoie les détails de l’exécution de flux nouvellement créée, y compris son exécution unique `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant de l’exécution de flux nouvellement créée. Consultez le guide sur la [récupération des spécifications de flux](../api/collect/database-nosql.md#specs) pour plus d’informations sur les spécifications d’exécution basées sur des tables. |
| `etag` | Version de ressource de l’exécution de flux. |

<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## Création d’une exécution de flux pour une source basée sur des fichiers

Pour créer un flux pour une source basée sur des fichiers, envoyez une requête de POST à l’API [!DNL Flow Service] tout en fournissant l’identifiant du flux sur lequel vous souhaitez créer l’exécution et les valeurs pour l’heure de début et l’heure de fin.

>[!TIP]
>
>Les sources basées sur des fichiers comprennent toutes les sources de stockage dans le cloud.

**Format d’API**

```http
POST /runs/
```

**Requête**

La requête suivante crée une exécution de flux pour l’ID de flux `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `flowId` | L’identifiant du flux sur lequel votre exécution de flux sera créée. |
| `params.startTime` | Heure planifiée du début de l’exécution du flux à la demande. Cette valeur est représentée en heure unique. |
| `params.windowStartTime` | Date et heure de récupération des données au plus tôt. Cette valeur est représentée en heure unique. |
| `params.windowEndTime` | Date et heure auxquelles les données seront récupérées. Cette valeur est représentée en heure unique. |

**Réponse**

Une réponse réussie renvoie les détails de l’exécution de flux nouvellement créée, y compris son exécution unique `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant de l’exécution de flux nouvellement créée. Consultez le guide sur la [récupération des spécifications de flux](../api/collect/database-nosql.md#specs) pour plus d’informations sur les spécifications d’exécution basées sur des tables. |
| `etag` | Version de ressource de l’exécution de flux. |

## Surveillance des exécutions de flux

Une fois l’exécution de flux créée, vous pouvez surveiller les données qui sont ingérées par celle-ci pour afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs. Pour surveiller les exécutions de flux à l’aide de l’API, consultez le tutoriel sur la [surveillance des flux de données dans l’API](./monitor.md). Pour surveiller les exécutions de flux à l’aide de l’interface utilisateur de Platform, consultez le guide sur la [surveillance des flux de données de sources à l’aide du tableau de bord de surveillance](../../../dataflows/ui/monitor-sources.md).
