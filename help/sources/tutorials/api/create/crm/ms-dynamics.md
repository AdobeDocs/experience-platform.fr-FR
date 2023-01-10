---
keywords: Experience Platform;accueil;rubriques populaires;Microsoft Dynamics;dynamique microsoft;dynamique;Dynamics
solution: Experience Platform
title: Création d’une connexion de base Microsoft Dynamics à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Platform à un compte Microsoft Dynamics à l’aide de l’API Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 53%

---

# Créez une connexion de base à [!DNL Microsoft Dynamics] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Microsoft Dynamics] (ci-après dénommés &quot;[!DNL Dynamics]&quot;) en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour connecter Platform à un compte Dynamics à l’aide de la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Dynamics], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUri` | L’URL du service de votre [!DNL Dynamics] instance. |
| `username` | Le nom d’utilisateur de votre [!DNL Dynamics] compte utilisateur. |
| `password` | Le mot de passe de votre [!DNL Dynamics] compte . |
| `servicePrincipalId` | L’ID client de votre [!DNL Dynamics] compte . Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Dynamics] est `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Pour plus d’informations sur la prise en main, voir [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Dynamics] dans les paramètres de la requête.

### Créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification de base

Pour créer une [!DNL Dynamics] connexion de base à l’aide de l’authentification de base, effectuez une requête de POST à l’adresse [!DNL Flow Service] API tout en fournissant des valeurs pour la connexion `serviceUri`, `username`, et `password`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | L’URI de service associé à votre [!DNL Dynamics] instance. |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Dynamics] compte . |
| `auth.params.password` | Le mot de passe associé à votre [!DNL Dynamics] compte . |
| `connectionSpec.id` | Le [!DNL Dynamics] identifiant de spécification de connexion : `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante. 

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Créez un [!DNL Dynamics] connexion de base à l’aide de l’authentification par clé principale de service

Pour créer une [!DNL Dynamics] connexion de base à l’aide de l’authentification par clé principale de service, envoyez une requête de POST à la fonction [!DNL Flow Service] API tout en fournissant des valeurs pour la connexion `serviceUri`, `servicePrincipalId`, et `servicePrincipalKey`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | L’URI de service associé à votre [!DNL Dynamics] instance. |
| `auth.params.servicePrincipalId` | L’ID client de votre [!DNL Dynamics] compte . Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `auth.params.servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `connectionSpec.id` | Le [!DNL Dynamics] identifiant de spécification de connexion : `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante. 

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Microsoft Dynamics] connexion de base à l’aide de [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de gestion de la relation client dans Platform à l’aide du [!DNL Flow Service] API](../../collect/crm.md)
