---
keywords: Experience Platform;accueil;rubriques populaires;eCommerce;eCommerce
solution: Experience Platform
title: Explorer une connexion eCommerce à l’aide de l’API Flow Service
description: Ce tutoriel utilise l’API Flow Service pour explorer les connexions eCommerce.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 35%

---

# Explorer une connexion eCommerce à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge peuvent être connectées.

Ce tutoriel utilise l’API [!DNL Flow Service] pour explorer une connexion **[!UICONTROL eCommerce]** tierce.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Sources]](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir la connexion à une connexion **[!UICONTROL eCommerce]** à l’aide de l’API [!DNL Flow Service].

### Obtention d’un identifiant de connexion

Pour explorer votre connexion **[!UICONTROL eCommerce]** à l’aide des API [!DNL Experience Platform], vous devez posséder un identifiant de connexion valide. Si vous ne disposez pas déjà d’une connexion pour la connexion **[!UICONTROL eCommerce]** que vous souhaitez utiliser, vous pouvez en créer une à l’aide du tutoriel suivant :

* [Shopify](../create/ecommerce/shopify.md)

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Explorer vos tableaux de données

À l’aide de votre identifiant de connexion **[!UICONTROL eCommerce]**, vous pouvez explorer vos tableaux de données en exécutant des requêtes GET. Utilisez l’appel suivant pour rechercher le chemin d’accès de la table que vous souhaitez inspecter ou ingérer dans [!DNL Experience Platform].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de tableaux de votre connexion **[!UICONTROL eCommerce]**. Recherchez la table que vous souhaitez importer dans [!DNL Experience Platform] et prenez note de sa propriété `path`, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

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

## Examiner la structure d’un tableau

Pour examiner la structure d’une table à partir de votre connexion **[!UICONTROL eCommerce]**, effectuez une requête GET tout en spécifiant le chemin d’accès d’une table dans un paramètre de requête `object`.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Identifiant de connexion de votre connexion **[!UICONTROL eCommerce]**. |
| `{TABLE_PATH}` | Chemin d’accès à une table dans votre connexion **[!UICONTROL eCommerce]**. |

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

Une réponse réussie renvoie la structure de la table spécifiée. Les détails concernant chacune des colonnes du tableau se trouvent dans les éléments du tableau `columns`.

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

En suivant ce tutoriel, vous avez exploré votre connexion **[!UICONTROL eCommerce]**, trouvé le chemin d’accès au tableau que vous souhaitez ingérer dans [!DNL Experience Platform] et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données e-commerce et les importer dans Experience Platform](../collect/ecommerce.md).
