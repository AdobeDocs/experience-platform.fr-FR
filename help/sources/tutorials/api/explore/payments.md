---
keywords: Experience Platform;accueil;rubriques les plus consultées;paiement
solution: Experience Platform
title: Exploration d’un système de paiement à l’aide de l’API Flow Service
topic-legacy: overview
description: Ce tutoriel utilise l’API Flow Service pour explorer les demandes de paiement.
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 35%

---

# Explorez un système de paiement à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] sert à collecter et à centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise l’API [!DNL Flow Service] pour explorer les demandes de paiement.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter avec succès à une application de paiements à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Ce tutoriel nécessite que vous disposiez d’une connexion valide avec l’application de paiements tierce à partir de laquelle vous souhaitez ingérer des données. Une connexion valide implique l’identifiant de spécification de connexion et l’identifiant de connexion de votre application. Vous trouverez plus d’informations sur la création d’une connexion aux paiements et la récupération de ces valeurs dans le tutoriel [Connexion d’une source de paiements à Platform](../../api/create/payments/paypal.md) .

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Exploration des tableaux de données

À l’aide de l’identifiant de connexion de votre système de paiements, vous pouvez explorer vos tableaux de données en exécutant des requêtes GET. Utilisez l’appel suivant pour trouver le chemin de la table que vous souhaitez inspecter ou ingérer dans [!DNL Platform].

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | L’identifiant d’une connexion de base de paiements. |

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

Une réponse réussie renvoie un tableau de tables de votre système de paiements. Recherchez le tableau que vous souhaitez importer dans [!DNL Platform] et notez sa propriété `path`, car vous devez le fournir à l’étape suivante pour inspecter sa structure.

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

Pour inspecter la structure d’une table à partir de votre système de paiements, effectuez une requête de GET tout en spécifiant le chemin d’une table comme paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | L’identifiant de connexion de votre système de paiements. |
| `{TABLE_PATH}` | Chemin d’accès d’une table dans votre système de paiements. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure de la table spécifiée. Les détails concernant chacune des colonnes du tableau sont situés dans les éléments du tableau `columns`.

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

En suivant ce tutoriel, vous avez exploré votre système de paiements, trouvé le chemin de la table que vous souhaitez ingérer dans [!DNL Platform] et obtenu des informations concernant sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données de votre système de paiements et les importer dans Platform](../collect/payments.md).
