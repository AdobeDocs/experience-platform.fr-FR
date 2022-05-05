---
keywords: Experience Platform;accueil;rubriques les plus consultées;sources;API;explorer;service de flux
title: Exploration d’une source tabulaire à l’aide de l’API Flow Service
description: Ce tutoriel utilise l’API Flow Service pour explorer le contenu et la structure d’une source basée sur un tableau.
source-git-commit: 1333eac5e022ef32f051120496154a88e2f9324e
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 23%

---

# Explorez les tableaux de données à l’aide du [!DNL Flow Service] API

Ce tutoriel décrit les étapes à suivre pour explorer et prévisualiser la structure et le contenu de vos tableaux de données à l’aide du [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
> Pour explorer vos tableaux de données, vous devez déjà disposer d’un identifiant de connexion de base valide pour une source tabulaire. Si vous ne possédez pas cet identifiant, consultez les tutoriels suivants pour savoir comment créer un identifiant de connexion de base pour une source tabulaire : <ul><li>[Publicité](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[Succès client](../../../home.md#customer-success)</li><li>[Base de données](../../../home.md#database)</li><li>[Commerce électronique](../../../home.md#ecommerce)</li><li>[Automatisation du marketing](../../../home.md#marketing-automation)</li><li>[Paiements](../../../home.md#payments)</li><li>[Protocoles](../../../home.md#protocols)</li></ul>

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../landing/api-guide.md).

## Exploration des tableaux de données

Vous pouvez récupérer des informations sur la structure de vos tableaux de données en adressant une requête GET à la variable [!DNL Flow Service] de l’API tout en fournissant l’identifiant de connexion de base de votre source.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base de votre source. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de tableaux de votre source. Recherchez la table que vous souhaitez importer dans Platform et notez ses `path` , car vous devez le fournir à l’étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la structure d’un tableau

Pour inspecter le contenu de vos tableaux de données, effectuez une requête GET à l’adresse [!DNL Flow Service] API lors de la spécification du chemin d’une table en tant que paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base de votre source. |
| `{TABLE_PATH}` | La propriété path de la table que vous souhaitez inspecter. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des informations sur le contenu et la structure du tableau spécifié. Les détails relatifs à chaque colonne du tableau se trouvent dans les éléments du `columns` tableau.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez rassemblé des informations sur la structure et le contenu de vos tableaux de données. De plus, vous avez récupéré le chemin d’accès à la table que vous souhaitez ingérer dans Platform. Vous pouvez utiliser ces informations pour créer une connexion source et un flux de données afin d’importer vos données dans Platform. Consultez les tutoriels suivants pour obtenir des instructions spécifiques sur la création d’une connexion source et d’un flux de données à l’aide du [!DNL Flow Service] API :

* [Sources publicitaires](../collect/advertising.md)
* [Sources CRM](../collect/crm.md)
* [Sources de succès client](../collect/customer-success.md)
* [Sources de base de données](../collect/database-nosql.md)
* [Sources de commerce électronique](../collect/ecommerce.md)
* [Sources d’automatisation du marketing](../collect/marketing-automation.md)
* [Sources de paiement](../collect/payments.md)
* [Sources de protocoles](../collect/protocols.md)