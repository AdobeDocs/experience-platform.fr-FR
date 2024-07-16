---
keywords: Experience Platform;accueil;rubriques populaires;Microsoft Dynamics;dynamique microsoft;dynamique;Dynamics
solution: Experience Platform
title: Création d’une connexion de base Microsoft Dynamics à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Platform à un compte Microsoft Dynamics à l’aide de l’API Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 55%

---

# Créez une connexion de base à [!DNL Microsoft Dynamics] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Microsoft Dynamics] (ci-après appelée &quot;[!DNL Dynamics]&quot;) à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour connecter Platform à un compte Dynamics à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Dynamics], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification de base]

| Informations d’identification | Description |
| --- | --- |
| `serviceUri` | URL du service de votre instance [!DNL Dynamics]. |
| `username` | Nom d’utilisateur de votre compte d’utilisateur [!DNL Dynamics]. |
| `password` | Mot de passe de votre compte [!DNL Dynamics]. |

>[!TAB  Authentification de clé et principal de service ]

| Informations d’identification | Description |
| --- | --- |
| `servicePrincipalId` | L’ID client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |

>[!ENDTABS]

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;une connexion de base [!DNL Dynamics]. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Dynamics] dans les paramètres de la requête.

### Création d’une connexion de base [!DNL Dynamics]

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;une connexion de base [!DNL Dynamics]. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL Dynamics] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL Dynamics] dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Authentification de base]

Pour créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification de base, envoyez une requête de POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour les `serviceUri`, `username` et `password` de votre connexion.

+++Requête

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
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Dynamics]. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Dynamics]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Dynamics] : `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

+++

+++Réponse

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante. 

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Authentification par clé principale de service]

Pour créer une connexion de base [!DNL Dynamics] à l’aide de l’authentification par clé principale de service, envoyez une requête de POST à l’API [!DNL Flow Service] tout en fournissant des valeurs pour les `serviceUri`, `servicePrincipalId` et `servicePrincipalKey` de votre connexion.

+++Requête

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
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | L’ID client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `auth.params.servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Dynamics] : `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

+++

+++Réponse

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante. 

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Microsoft Dynamics] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de gestion de la relation client dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/crm.md)
