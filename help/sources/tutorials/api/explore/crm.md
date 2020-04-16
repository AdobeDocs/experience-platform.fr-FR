---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exploration d’un système CRM à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: 3d8682eb1a33b7678ed814e5d6d2cb54d233c03e

---


# Exploration d’un système CRM à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API Flow Service pour explorer les systèmes CRM.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système CRM à l’aide de l’API du service de flux.

### Obtention d’une connexion de base

Pour explorer votre système de gestion de la relation client à l’aide des API de plateforme, vous devez posséder un ID de connexion de base valide. Si vous ne disposez pas déjà d’une connexion de base pour le système CRM avec lequel vous souhaitez travailler, vous pouvez en créer une à l’aide des didacticiels suivants :

* [Microsoft Dynamics](../create/crm/ms-dynamics.md)
* [Salesforce](../create/crm/salesforce.md)

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

## Explorez vos tableaux de données

En utilisant la connexion de base pour votre système de gestion de la relation client, vous pouvez explorer vos tableaux de données en exécutant des requêtes GET. Utilisez l&#39;appel suivant pour trouver le chemin du tableau que vous souhaitez inspecter ou assimiler dans Platform.

**Format API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de la connexion de base pour votre système CRM. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive est un tableau de tableaux de votre système de gestion de la relation client. Trouvez la table que vous souhaitez amener dans Plateforme et prenez note de sa `path` propriété, comme vous devez le fournir dans l&#39;étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "Solution Component Summary",
        "path": "msdyn_solutioncomponentsummary",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Quote Invoicing Product",
        "path": "msdyn_quoteinvoicingproduct",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Opportunity Relationship",
        "path": "customeropportunityrole",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Vérification de la structure d’un tableau

Pour inspecter la structure d&#39;une table à partir de votre système CRM, effectuez une requête GET tout en spécifiant le chemin d&#39;une table comme paramètre de .

**Format API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de la connexion de base pour votre système CRM. |
| `{TABLE_PATH}` | Chemin d’accès d’un tableau. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure d’un tableau. Les détails concernant chacune des colonnes du tableau sont situés dans les éléments du `columns` tableau.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre système CRM, trouvé le chemin du tableau que vous souhaitez apporter à Platform, et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter les données de votre système de gestion de la relation client et les importer dans Platform](../collect/crm.md).