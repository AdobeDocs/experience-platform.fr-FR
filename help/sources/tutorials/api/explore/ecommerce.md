---
keywords: Experience Platform ; accueil ; rubriques populaires ; commerce électronique ; commerce électronique
solution: Experience Platform
title: Exploration d’une connexion au commerce électronique à l’aide de l’API du service de flux
topic-legacy: overview
description: Ce didacticiel utilise l’API Flow Service pour explorer les connexions eCommerce.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 25%

---

# Explorez une connexion eCommerce à l&#39;aide de l&#39;API [!DNL Flow Service]

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour explorer une connexion **[!UICONTROL eCommerce]** tierce.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Sources]](../../../home.md):  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md):  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à une connexion **[!UICONTROL eCommerce]** à l&#39;aide de l&#39;API [!DNL Flow Service].

### Obtention d’un ID de connexion

Pour explorer votre connexion **[!UICONTROL eCommerce]** à l&#39;aide des API [!DNL Platform], vous devez posséder un ID de connexion valide. Si vous n&#39;avez pas encore de connexion pour la connexion **[!UICONTROL eCommerce]** que vous souhaitez utiliser, vous pouvez en créer une à l&#39;aide du didacticiel suivant :

* [Shopify](../create/ecommerce/shopify.md)

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

En utilisant votre ID de connexion **[!UICONTROL eCommerce]**, vous pouvez explorer vos tableaux de données en exécutant des requêtes de GET. Utilisez l&#39;appel suivant pour trouver le chemin de la table que vous souhaitez inspecter ou assimiler dans [!DNL Platform].

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{CONNECTION_ID}` | Votre identifiant de connexion **[!UICONTROL eCommerce]**. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Pour inspecter la structure d&#39;une table à partir de votre connexion **[!UICONTROL eCommerce]**, effectuez une demande de GET tout en spécifiant le chemin d&#39;une table dans un paramètre de requête `object`.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | ID de connexion de votre connexion **[!UICONTROL eCommerce]**. |
| `{TABLE_PATH}` | Chemin d’accès d’une table dans votre connexion **[!UICONTROL eCommerce]**. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure de la table spécifiée. Les détails relatifs à chacune des colonnes du tableau se trouvent dans les éléments du tableau `columns`.

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

En suivant ce tutoriel, vous avez exploré votre connexion **[!UICONTROL eCommerce]**, trouvé le chemin du tableau que vous souhaitez insérer dans [!DNL Platform] et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter des données de commerce électronique et les importer dans Platform](../collect/ecommerce.md).
