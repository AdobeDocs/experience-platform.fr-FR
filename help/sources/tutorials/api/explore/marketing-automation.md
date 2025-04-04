---
keywords: Experience Platform;accueil;rubriques populaires;automatisation du marketing
solution: Experience Platform
title: Explorer un système d’automatisation du marketing à l’aide de l’API Flow Service
description: Ce tutoriel utilise l’API Flow Service pour explorer les systèmes d’automatisation du marketing.
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 37%

---

# Explorer un système d’automatisation du marketing à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge peuvent être connectées.

Ce tutoriel utilise l’API [!DNL Flow Service] pour explorer les systèmes d’automatisation du marketing.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à un système d’automatisation marketing à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Ce tutoriel nécessite une connexion valide avec l’application d’automatisation marketing tierce à partir de laquelle vous souhaitez ingérer des données. Une connexion valide implique l’identifiant de spécification de connexion et l’identifiant de connexion de votre application. Vous trouverez plus d’informations sur la création d’une connexion d’automatisation marketing et la récupération de ces valeurs dans le tutoriel [connecter une source d’automatisation marketing à Experience Platform](../../api/create/marketing-automation/hubspot.md).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Explorer vos tableaux de données

En utilisant la connexion de base de votre système d’automatisation marketing, vous pouvez explorer vos tableaux de données en exécutant des requêtes GET. Utilisez l’appel suivant pour rechercher le chemin d’accès de la table que vous souhaitez inspecter ou ingérer dans [!DNL Experience Platform].

**Format d’API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de la connexion de base pour votre système d’automatisation marketing. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie est un tableau de tables de vers votre système d’automatisation du marketing. Recherchez la table que vous souhaitez importer dans [!DNL Experience Platform] et prenez note de sa propriété `path`, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## Examiner la structure d’un tableau

Pour inspecter la structure d’une table à partir de votre système d’automatisation marketing, effectuez une requête GET tout en spécifiant le chemin d’accès d’une table comme paramètre de requête.

**Format d’API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de votre système d’automatisation marketing. |
| `{TABLE_PATH}` | Chemin d’accès d’une table dans votre système d’automatisation marketing. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure d’un tableau. Les détails concernant chacune des colonnes du tableau se trouvent dans les éléments du tableau `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre système d’automatisation marketing, trouvé le chemin d’accès au tableau que vous souhaitez importer dans [!DNL Experience Platform] et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données à partir de votre système d’automatisation du marketing et les importer dans Experience Platform](../collect/marketing-automation.md).
