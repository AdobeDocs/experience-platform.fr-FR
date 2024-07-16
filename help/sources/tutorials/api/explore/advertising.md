---
keywords: Experience Platform;accueil;rubriques populaires;système publicitaire;système Advertising
solution: Experience Platform
title: Exploration d’un système Advertising à l’aide de l’API Flow Service
description: Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables. Ce tutoriel utilise l’API Flow Service pour explorer les systèmes publicitaires.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 19%

---

# Explorez un système publicitaire à l’aide de l’API [!DNL Flow Service]

Une fois la connexion de base créée, vous pouvez désormais utiliser l’identifiant de connexion de base unique pour parcourir la structure de données et le contenu de votre source. Vous pouvez ainsi identifier les éléments spécifiques, ainsi que leurs types de données et formats respectifs, avant de créer un flux de données et de les transférer à Adobe Experience Platform.

Ce tutoriel utilise l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) pour explorer les systèmes publicitaires.

## Commencer

>[!IMPORTANT]
>
>Ce tutoriel nécessite que vous disposiez de l’identifiant de connexion de base unique pour votre source publicitaire. Si vous ne possédez pas cet identifiant, consultez le tutoriel sur la [connexion d’une source publicitaire à Platform](../../api/create/advertising/ads.md) .

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système publicitaire à l’aide de l’API [!DNL Flow Service].

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../landing/api-guide.md).

## Exploration des tableaux de données

À l’aide de la connexion de base de votre système publicitaire, vous pouvez explorer vos tableaux de données en exécutant des requêtes GET. Utilisez l’appel suivant pour trouver le chemin de la table que vous souhaitez inspecter ou ingérer dans [!DNL Platform].

**Format d’API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | L’identifiant de la connexion de base de votre système publicitaire. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie est un tableau de tableaux allant de à votre système publicitaire. Recherchez la table que vous souhaitez importer dans [!DNL Platform] et notez sa propriété `path`, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la structure d’un tableau

Pour inspecter la structure d’une table à partir de votre système publicitaire, effectuez une requête de GET tout en spécifiant le chemin d’une table comme paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de votre système publicitaire. |
| `{TABLE_PATH}` | Chemin d’accès d’un tableau dans votre système publicitaire. |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure d’un tableau. Les détails concernant chacune des colonnes de la table se trouvent dans les éléments du tableau `columns`.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre système publicitaire, trouvé le chemin de la table que vous souhaitez importer dans [!DNL Platform] et obtenu des informations sur sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données de votre système publicitaire et les importer dans Platform](../collect/advertising.md).
