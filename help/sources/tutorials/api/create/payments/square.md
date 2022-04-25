---
keywords: Experience Platform;accueil;rubriques les plus consultées;Carré;carré
title: Création d’une connexion de base carrée à l’aide de l’API Flow Service
description: Découvrez comment connecter Square à Adobe Experience Platform à l’aide de l’API Flow Service.
source-git-commit: f2f602fd618dc6b59ba13c275ca0c2964e3ea1f4
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 48%

---

# Créez une connexion de base à [!DNL Square] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Square] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Environnements de test](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Square] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Square], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `host` | L’URL de la variable [!DNL Square] instance. |
| `clientId` | L’ID client associé à votre [!DNL Square] compte . |
| `clientSecret` | Le secret client associé à votre [!DNL Square] compte . |
| `accessToken` | Le jeton d’accès est utilisé pour authentifier votre [!DNL Square] compte avec authentification OAuth 2.0. Le jeton d’accès peut être obtenu à partir de [!DNL Square]. |
| `refreshToken` | Le jeton d’actualisation est utilisé pour générer de nouveaux jetons d’accès une fois que votre jeton d’accès actuel expire. Le jeton d’actualisation peut être obtenu à partir de [!DNL Square]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Square] est : `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Pour plus d’informations sur ces informations d’identification et sur la manière de les obtenir, reportez-vous à la section [[!DNL Square] documentation sur OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | L’URL de la variable [!DNL Square] instance. |
| `auth.params.clientId` | L’ID client associé à votre [!DNL Square] compte . |
| `auth.params.clientSecret` | Le secret client associé à votre [!DNL Square] compte . |
| `auth.params.accessToken` | Le jeton d’accès est utilisé pour authentifier votre [!DNL Square] compte avec authentification OAuth 2.0. Le jeton d’accès peut être obtenu à partir de [!DNL Square]. |
| `auth.params.refreshToken` | Le jeton d’actualisation est utilisé pour générer de nouveaux jetons d’accès une fois que votre jeton d’accès actuel expire. Le jeton d’actualisation peut être obtenu à partir de [!DNL Square]. |
| `connectionSpec.id` | Le [!DNL Square] identifiant de spécification de connexion : `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de , y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Square] connexion à l’aide de la fonction [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer l’application de paiements à l’aide de l’API Flow Service](../../explore/payments.md).
