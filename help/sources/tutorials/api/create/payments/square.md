---
keywords: Experience Platform;accueil;rubriques les plus consultées;Carré;carré
title: Création d’une connexion de base carrée à l’aide de l’API Flow Service
description: Découvrez comment connecter Square à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 45%

---

# Créez une connexion de base à [!DNL Square] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Square] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Square] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Square], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `host` | URL de l’instance [!DNL Square]. |
| `clientId` | L’ID client associé à votre compte [!DNL Square]. |
| `clientSecret` | Le secret client associé à votre compte [!DNL Square]. |
| `accessToken` | Le jeton d’accès est utilisé pour authentifier votre compte [!DNL Square] avec l’authentification OAuth 2.0. Le jeton d’accès peut être obtenu à partir de [!DNL Square]. |
| `refreshToken` | Le jeton d’actualisation est utilisé pour générer de nouveaux jetons d’accès une fois que votre jeton d’accès actuel expire. Le jeton d’actualisation peut être obtenu à partir de [!DNL Square]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Square] est : `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Pour plus d’informations sur ces informations d’identification et sur la manière de les obtenir, consultez la [[!DNL Square] documentation sur OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Square] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Square] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | URL de l’instance [!DNL Square]. |
| `auth.params.clientId` | L’ID client associé à votre compte [!DNL Square]. |
| `auth.params.clientSecret` | Le secret client associé à votre compte [!DNL Square]. |
| `auth.params.accessToken` | Le jeton d’accès est utilisé pour authentifier votre compte [!DNL Square] avec l’authentification OAuth 2.0. Le jeton d’accès peut être obtenu à partir de [!DNL Square]. |
| `auth.params.refreshToken` | Le jeton d’actualisation est utilisé pour générer de nouveaux jetons d’accès une fois que votre jeton d’accès actuel expire. Le jeton d’actualisation peut être obtenu à partir de [!DNL Square]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Square] : `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Square] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer l&#39;application de paiements à l&#39;aide de l&#39;API Flow Service](../../explore/payments.md).
