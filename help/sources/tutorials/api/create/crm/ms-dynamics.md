---
keywords: Experience Platform;accueil;rubriques les plus consultées;Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Création d’une connexion de base Microsoft Dynamics à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Platform à un compte Microsoft Dynamics à l’aide de l’API Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 9%

---

# Créez une connexion de base [!DNL Microsoft Dynamics] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Microsoft Dynamics] (ci-après appelée &quot;[!DNL Dynamics]&quot;) à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour connecter Platform à un compte Dynamics à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Dynamics], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `serviceUri` | URL du service de votre instance [!DNL Dynamics]. |
| `username` | Nom d’utilisateur de votre compte d’utilisateur [!DNL Dynamics]. |
| `password` | Mot de passe de votre compte [!DNL Dynamics]. |
| `servicePrincipalId` | Identifiant client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Dynamics] est : `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Pour plus d’informations sur la prise en main, consultez [ce [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Dynamics] dans le cadre des paramètres de requête.

### Créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification de base

Pour créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification de base, envoyez une requête de POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour les `serviceUri`, `username` et `password` de votre connexion.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Dynamics]. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Dynamics]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Dynamics] : `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification par clé principale de service

Pour créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification par clé principale de service, envoyez une requête de POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour les `serviceUri`, `servicePrincipalId` et `servicePrincipalKey` de votre connexion.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | Identifiant client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `auth.params.servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Dynamics] : `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Dynamics] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer les systèmes de gestion de la relation client à l’aide de l’API Flow Service](../../explore/crm.md).
