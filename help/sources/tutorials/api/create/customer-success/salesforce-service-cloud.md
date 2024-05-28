---
title: Création d’une connexion à la source cloud du service Salesforce à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Salesforce Service Cloud à l’aide de l’API Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 33%

---

# Créez un [!DNL Salesforce Service Cloud] connexion source à l’aide de la fonction [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Lisez ce tutoriel pour savoir comment créer une connexion de base pour [!DNL Salesforce Service Cloud] en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md): l’Experience Platform fournit des environnements de test virtuels qui divisent une seule [!DNL Platform] dans des environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Salesforce Service Cloud] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

La variable [!DNL Salesforce Service Cloud] source prend en charge l’authentification de base et les informations d’identification du client OAuth2.

>[!BEGINTABS]

>[!TAB Authentification de base]

Pour connecter votre [!DNL Salesforce Service Cloud] compte à [!DNL Flow Service] à l’aide de l’authentification de base, indiquez les valeurs des informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | L’URL de la variable [!DNL Salesforce Service Cloud] instance source. |
| `username` | Nom d’utilisateur de la variable [!DNL Salesforce Service Cloud] compte utilisateur. |
| `password` | Le mot de passe du [!DNL Salesforce Service Cloud] compte utilisateur. |
| `securityToken` | Jeton de sécurité pour la variable [!DNL Salesforce Service Cloud] compte utilisateur. |
| `apiVersion` | (Facultatif) La version de l’API REST de la variable [!DNL Salesforce Service Cloud] que vous utilisez. La valeur de la version de l’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur sous la forme `52.0`. Si ce champ n’est pas renseigné, l’Experience Platform utilisera automatiquement la dernière version disponible. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce Service Cloud] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d’informations sur la prise en main, voir [ce document Salesforce ;](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Informations d’identification du client OAuth 2]

Pour connecter votre [!DNL Salesforce Service Cloud] compte à [!DNL Flow Service] à l’aide des informations d’identification du client OAuth 2, indiquez les valeurs des informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | L’URL de la variable [!DNL Salesforce Service Cloud] instance source. |
| `clientId` | L’ID client est utilisé en tandem avec le secret client dans le cadre de l’authentification OAuth2. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre client en identifiant votre application à [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Le secret client est utilisé en tandem avec l’ID client dans le cadre de l’authentification OAuth2. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre client en identifiant votre application à [!DNL Salesforce Service Cloud]. |
| `apiVersion` | La version de l’API REST de la variable [!DNL Salesforce Service Cloud] que vous utilisez. La valeur de la version de l’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur sous la forme `52.0`. Si ce champ n’est pas renseigné, l’Experience Platform utilisera automatiquement la dernière version disponible. Cette valeur est obligatoire pour l’authentification des informations d’identification du client OAuth2. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce Service Cloud] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d’informations sur l’utilisation d’OAuth pour [!DNL Salesforce Service Cloud], lisez le [[!DNL Salesforce Service Cloud] Guide sur les flux d’autorisation OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Salesforce Service Cloud] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

>[!BEGINTABS]

>[!TAB Authentification de base]

La requête suivante crée une connexion de base pour [!DNL Salesforce Service Cloud] à l’aide de l’authentification de base :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Paramètre | Description |
| ---| --- |
| `auth.params.environmentUrl` | L’URL de votre [!DNL Salesforce Service Cloud] instance. |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Salesforce Service Cloud] compte . |
| `auth.params.password` | Le mot de passe associé à votre [!DNL Salesforce Service Cloud] compte . |
| `auth.params.securityToken` | Le jeton de sécurité associé à votre [!DNL Salesforce Service Cloud] compte . |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Salesforce Service Cloud] : `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!TAB Informations d’identification du client OAuth2]

La requête suivante crée une connexion de base pour [!DNL Salesforce Service Cloud] à l’aide des informations d’identification du client OAuth 2 :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.environmentUrl` | L’URL de votre [!DNL Salesforce Service Cloud] instance. |
| `auth.params.clientId` | L’ID client associé à votre [!DNL Salesforce Service Cloud] compte . |
| `auth.params.clientSecret` | Le secret client associé à votre [!DNL Salesforce Service Cloud] compte . |
| `auth.params.apiVersion` | La version de l’API REST de la variable [!DNL Salesforce Service Cloud] que vous utilisez. |
| `connectionSpec.id` | La variable [!DNL Salesforce Service Cloud] identifiant de spécification de connexion : `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Réponse**

Une réponse réussie renvoie votre nouvelle connexion de base, ainsi que son identifiant unique.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Salesforce Service Cloud] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de succès client dans Platform à l’aide de l’API  [!DNL Flow Service] .](../../collect/customer-success.md)
