---
keywords: Experience Platform;accueil;rubriques les plus consultées;commerce électronique;commerce électronique
solution: Experience Platform
title: Exploration d’une connexion eCommerce à l’aide de l’API Flow Service
description: Ce tutoriel utilise l’API Flow Service pour explorer les connexions eCommerce.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 35%

---

# Exploration d’une connexion eCommerce à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] est utilisé pour collecter et centraliser des données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise l’API [!DNL Flow Service] pour explorer une connexion **[!UICONTROL eCommerce]** tierce.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Sources]](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [[!DNL Sandboxes]](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à une connexion **[!UICONTROL eCommerce]** à l’aide de l’API [!DNL Flow Service].

### Obtention d’un identifiant de connexion

Pour explorer votre connexion **[!UICONTROL eCommerce]** à l’aide des API [!DNL Platform], vous devez posséder un identifiant de connexion valide. Si vous n’avez pas encore de connexion pour la connexion **[!UICONTROL eCommerce]** que vous souhaitez utiliser, vous pouvez en créer une via le tutoriel suivant :

* [Shopify](../create/ecommerce/shopify.md)

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Exploration des tableaux de données

À l’aide de votre ID de connexion **[!UICONTROL eCommerce]**, vous pouvez explorer vos tableaux de données en exécutant des requêtes de GET. Utilisez l’appel suivant pour trouver le chemin de la table que vous souhaitez inspecter ou ingérer dans [!DNL Platform].

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{CONNECTION_ID}` | Votre ID de connexion **[!UICONTROL eCommerce]**. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de tables de votre connexion **[!UICONTROL eCommerce]**. Recherchez la table que vous souhaitez importer dans [!DNL Platform] et notez sa propriété `path`, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la structure d’un tableau

Pour inspecter la structure d’une table à partir de votre connexion **[!UICONTROL eCommerce]**, effectuez une requête de GET tout en spécifiant le chemin d’accès d’une table dans un paramètre de requête `object`.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | L’identifiant de connexion de votre connexion **[!UICONTROL eCommerce]**. |
| `{TABLE_PATH}` | Chemin d’accès d’une table dans votre connexion **[!UICONTROL eCommerce]**. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure de la table spécifiée. Les détails concernant chacune des colonnes de la table se trouvent dans les éléments du tableau `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre connexion **[!UICONTROL eCommerce]**, trouvé le chemin de la table que vous souhaitez ingérer dans [!DNL Platform] et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données eCommerce et les importer dans Platform](../collect/ecommerce.md).
