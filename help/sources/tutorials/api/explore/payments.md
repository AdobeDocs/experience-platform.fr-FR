---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Explorez un système de paiement à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 16%

---


# Explorez un système de paiement à l’aide de l’ [!DNL Flow Service] API

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates au sein de l’Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39; [!DNL Flow Service] API pour explorer les applications de paiement.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to a payments application using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Ce didacticiel nécessite que vous disposiez d’une connexion valide avec l’application de paiement tierce à partir de laquelle vous souhaitez importer des données. Une connexion valide implique l&#39;ID de spécification de connexion et l&#39;ID de connexion de votre application. Pour plus d&#39;informations sur la création d&#39;une connexion aux paiements et la récupération de ces valeurs, consultez le didacticiel [Connexion d&#39;une source de paiement à Platform](../../api/create/payments/paypal.md) .

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Explorez vos tableaux de données

A l’aide de l’ID de connexion de votre système de paiement, vous pouvez explorer vos tableaux de données en exécutant des requêtes de GET. Utilisez l&#39;appel suivant pour trouver le chemin du tableau que vous souhaitez inspecter ou intégrer [!DNL Platform].

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d&#39;une connexion de base de paiements. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de tables de votre système de paiements. Trouvez la table que vous souhaitez introduire [!DNL Platform] et prenez note de sa `path` propriété, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "PayPal.Billing_Plans",
        "path": "PayPal.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Billing_Plans_Payment_Definition",
        "path": "PayPal.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "PayPal.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Catalog_Products",
        "path": "PayPal.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la structure d’un tableau

Pour inspecter la structure d&#39;une table à partir de votre système de paiements, effectuez une demande de GET tout en spécifiant le chemin d&#39;une table en tant que paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID de connexion de votre système de paiements. |
| `{TABLE_PATH}` | Chemin d&#39;accès d&#39;une table dans votre système de paiements. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure de la table spécifiée. Les détails concernant chacune des colonnes du tableau se trouvent dans les éléments du `columns` tableau.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
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

En suivant ce tutoriel, vous avez exploré votre système de paiements, trouvé le chemin du tableau dans lequel vous souhaitez insérer [!DNL Platform], et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter des données à partir de votre système de paiement et les importer dans Platform](../collect/payments.md).