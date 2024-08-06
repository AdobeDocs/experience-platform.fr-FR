---
title: Création d’une connexion de base Salesforce à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte Salesforce à l’aide de l’API Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 5951b0f549c2fd2723945f8f4089d12f73b92e6c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 36%

---

# Créez une connexion de base à [!DNL Salesforce] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Salesforce] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour connecter [!DNL Platform] à un compte [!DNL Salesforce] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

La source [!DNL Salesforce] prend en charge l’authentification de base et les informations d’identification du client OAuth2.

>[!BEGINTABS]

>[!TAB Authentification de base]

Pour connecter votre compte [!DNL Salesforce] à [!DNL Flow Service] à l’aide de l’authentification de base, indiquez les valeurs des informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | URL de l’instance source [!DNL Salesforce]. Le format de `environmentUrl` est `https://[domain].my.salesforce.com`. |
| `username` | Nom d’utilisateur du compte utilisateur [!DNL Salesforce]. |
| `password` | Mot de passe du compte utilisateur [!DNL Salesforce]. |
| `securityToken` | Jeton de sécurité pour le compte utilisateur [!DNL Salesforce]. |
| `apiVersion` | (Facultatif) La version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. La valeur de la version de l’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Informations d’identification du client OAuth 2]

Pour connecter votre compte [!DNL Salesforce] à [!DNL Flow Service] à l’aide des informations d’identification client OAuth 2, indiquez les valeurs des informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | URL de l’instance source [!DNL Salesforce]. Le format de `environmentUrl` est `https://[domain].my.salesforce.com` |
| `clientId` | L’ID client est utilisé en tandem avec le secret client dans le cadre de l’authentification OAuth2. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application sur [!DNL Salesforce]. |
| `clientSecret` | Le secret client est utilisé en tandem avec l’ID client dans le cadre de l’authentification OAuth2. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application sur [!DNL Salesforce]. |
| `apiVersion` | Version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. La valeur de la version de l’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. Cette valeur est obligatoire pour l’authentification des informations d’identification du client OAuth2. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d’informations sur l’utilisation d’OAuth pour [!DNL Salesforce], consultez le [[!DNL Salesforce] guide sur les flux d’autorisation OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` et fournissez vos informations d’identification d’authentification [!DNL Salesforce] dans le corps de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

>[!BEGINTABS]

>[!TAB Authentification de base]

La requête suivante crée une connexion de base pour [!DNL Salesforce] à l’aide de l’authentification de base :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.environmentUrl` | URL de votre instance [!DNL Salesforce]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Salesforce]. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Salesforce]. |
| `auth.params.securityToken` | Jeton de sécurité associé à votre compte [!DNL Salesforce]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Salesforce] : `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB Informations d’identification du client OAuth 2]

La requête suivante crée une connexion de base pour [!DNL Salesforce] à l’aide des informations d’identification client OAuth 2 :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
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
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.environmentUrl` | URL de votre instance [!DNL Salesforce]. |
| `auth.params.clientId` | L’ID client associé à votre compte [!DNL Salesforce]. |
| `auth.params.clientSecret` | Le secret client associé à votre compte [!DNL Salesforce]. |
| `auth.params.apiVersion` | Version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Salesforce] : `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Réponse**

Une réponse réussie renvoie votre nouvelle connexion de base, ainsi que son identifiant unique.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Salesforce] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de gestion de la relation client dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/crm.md)
