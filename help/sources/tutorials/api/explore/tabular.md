---
keywords: Experience Platform;accueil;rubriques populaires;sources;API;explorer;flow service
title: Explorer un Source tabulaire à l’aide de l’API Flow Service
description: Ce tutoriel utilise l’API Flow Service pour explorer le contenu et la structure d’une source basée sur des tableaux.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 16%

---

# Explorer des tableaux de données à l’aide de l’API [!DNL Flow Service]

Ce tutoriel décrit les étapes à suivre pour explorer et prévisualiser la structure et le contenu de vos tableaux de données à l’aide de l’API [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Pour explorer vos tables de données, vous devez déjà disposer d’un identifiant de connexion de base valide pour une source tabulaire. Si vous ne disposez pas de cet identifiant, consultez les tutoriels suivants pour savoir comment créer un identifiant de connexion de base pour une source tabulaire : <ul><li>[Publicité](../../../home.md#advertising)</li><li>[&#x200B; CRM &#x200B;](../../../home.md#customer-relationship-management)</li><li>[Succès client](../../../home.md#customer-success)</li><li>[Base de données](../../../home.md#database)</li><li>[E-commerce](../../../home.md#ecommerce)</li><li>[Automatisation du marketing](../../../home.md#marketing-automation)</li><li>[&#x200B; Paiements &#x200B;](../../../home.md#payments)</li><li>[Protocoles](../../../home.md#protocols)</li></ul>

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../landing/api-guide.md).

## Explorer vos tableaux de données

Vous pouvez récupérer des informations sur la structure de vos tableaux de données en adressant une requête GET à l’API [!DNL Flow Service] et en fournissant l’identifiant de connexion de base de votre source.

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

Une réponse réussie renvoie un tableau de tableaux de votre source. Recherchez le tableau que vous souhaitez importer dans Experience Platform et prenez note de sa propriété `path`, car vous devez la fournir à l’étape suivante pour examiner sa structure.

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

## Examiner la structure d’un tableau

Pour examiner le contenu de vos tables de données, envoyez une requête GET à l’API [!DNL Flow Service] tout en spécifiant le chemin d’accès d’une table comme paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base de votre source. |
| `{TABLE_PATH}` | Propriété de chemin d&#39;accès de la table à inspecter. |

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

Une réponse réussie renvoie des informations sur le contenu et la structure de la table spécifiée. Les détails concernant chacune des colonnes du tableau se trouvent dans les éléments du tableau `columns`.

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

En suivant ce tutoriel, vous avez rassemblé des informations sur la structure et le contenu de vos tableaux de données. De plus, vous avez récupéré le chemin d’accès à la table que vous souhaitez ingérer dans Experience Platform. Vous pouvez utiliser ces informations pour créer une connexion source et un flux de données afin d’importer vos données dans Experience Platform. Pour obtenir des instructions spécifiques sur la création d’une connexion source et d’un flux de données à l’aide de l’API [!DNL Flow Service], consultez les tutoriels suivants :

* [Sources Advertising](../collect/advertising.md)
* [Sources CRM](../collect/crm.md)
* [Sources de succès du client](../collect/customer-success.md)
* [Sources de base de données](../collect/database-nosql.md)
* [Sources d’e-commerce](../collect/ecommerce.md)
* [Sources d’automatisation du marketing](../collect/marketing-automation.md)
* [Sources de paiements](../collect/payments.md)
* [Sources des protocoles](../collect/protocols.md)
