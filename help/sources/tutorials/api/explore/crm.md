---
keywords: Experience Platform;accueil;rubriques populaires;CRM;crm;crm flow service
solution: Experience Platform
title: Explorez un système CRM à l’aide de l’API du service de flux
topic-legacy: overview
description: Ce didacticiel utilise l’API Flow Service pour explorer les systèmes CRM.
exl-id: 9a8c553a-a93d-4539-a9d2-5f76a3927d92
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 25%

---

# Explorez un système de gestion de la relation client à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour explorer les systèmes de gestion de la relation client.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système de gestion de la relation client à l&#39;aide de l&#39;API [!DNL Flow Service].

### Création d’un ID de connexion

Pour explorer votre système de gestion de la relation client à l&#39;aide des API [!DNL Platform], vous devez posséder un ID de connexion valide. Si vous n’avez pas encore de connexion au système de gestion de la relation client que vous souhaitez utiliser, vous pouvez en créer une à l’aide des didacticiels suivants :

* [Microsoft Dynamics ](../create/crm/ms-dynamics.md)
* [Salesforce](../create/crm/salesforce.md)

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Explorez vos tableaux de données

L’ID de connexion de votre système de gestion de la relation client vous permet d’explorer vos tableaux de données en exécutant des requêtes de GET. Utilisez l&#39;appel suivant pour trouver le chemin de la table que vous souhaitez inspecter ou assimiler dans [!DNL Platform].

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de la connexion de base pour votre système de gestion de la relation client. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive est un ensemble de tables de votre système de gestion de la relation client. Recherchez la table que vous souhaitez importer dans [!DNL Platform] et notez sa propriété `path`, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

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

## Inspect de la structure d’un tableau

Pour inspecter la structure d&#39;une table à partir de votre système de gestion de la relation client, effectuez une demande de GET tout en spécifiant le chemin d&#39;une table en tant que paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de la connexion de base pour votre système de gestion de la relation client. |
| `{TABLE_PATH}` | Chemin d’accès d’un tableau. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure d’un tableau. Les détails relatifs à chacune des colonnes du tableau se trouvent dans les éléments du tableau `columns`.

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

En suivant ce tutoriel, vous avez exploré votre système de gestion de la relation client, trouvé le chemin du tableau que vous souhaitez apporter à [!DNL Platform] et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter les données de votre système de gestion de la relation client et les importer dans Platform](../collect/crm.md).
