---
title: Connecter Salesforce à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte Salesforce à l’aide de l’API Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 19%

---

# Connexion de [!DNL Salesforce] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre compte source [!DNL Salesforce] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Connexion de [!DNL Salesforce] à Experience Platform sur [!DNL Azure] {#azure}

Pour plus d’informations sur la connexion de votre source [!DNL Salesforce] à Experience Platform on [!DNL Azure], lisez les étapes ci-dessous.

### Collecter les informations d’identification requises

La source [!DNL Salesforce] prend en charge l’authentification de base et les informations d’identification du client OAuth2.

>[!BEGINTABS]

>[!TAB  Authentification de base ]

Pour connecter votre compte [!DNL Salesforce] à [!DNL Flow Service] à l’aide de l’authentification de base, saisissez des valeurs pour les informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | URL de l’instance source de la [!DNL Salesforce]. Le format de `environmentUrl` est `https://[domain].my.salesforce.com`. |
| `username` | Nom d’utilisateur du compte utilisateur [!DNL Salesforce]. |
| `password` | Mot de passe du compte utilisateur [!DNL Salesforce]. |
| `securityToken` | Jeton de sécurité du compte utilisateur [!DNL Salesforce]. |
| `apiVersion` | (Facultatif) Version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. La valeur de la version de l’API doit être formatée avec une décimale. Par exemple, si vous utilisez la version `52` de l’API, vous devez saisir la valeur comme `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilise automatiquement la dernière version disponible. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d’informations sur la prise en main, consultez [ce document Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB  Informations d’identification du client OAuth 2 ]

Pour connecter votre compte [!DNL Salesforce] à [!DNL Flow Service] à l’aide des informations d’identification du client OAuth 2, saisissez des valeurs pour les informations d’identification suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | URL de l’instance source de la [!DNL Salesforce]. Le format de `environmentUrl` est `https://[domain].my.salesforce.com` |
| `clientId` | L’identifiant client est utilisé conjointement avec le secret client dans le cadre de l’authentification OAuth2. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Salesforce]. |
| `clientSecret` | Le secret client est utilisé conjointement avec l’identifiant client dans le cadre de l’authentification OAuth2. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Salesforce]. |
| `apiVersion` | Version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. La valeur de la version de l’API doit être formatée avec une décimale. Par exemple, si vous utilisez la version `52` de l’API, vous devez saisir la valeur comme `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilise automatiquement la dernière version disponible. Cette valeur est obligatoire pour l’authentification des informations d’identification du client OAuth2. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d’informations sur l’utilisation d’OAuth pour [!DNL Salesforce], consultez le guide [[!DNL Salesforce]  sur les flux d’autorisation OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Créer une connexion de base pour [!DNL Salesforce] dans Experience Platform sur [!DNL Azure]

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer une connexion de base et connecter votre compte [!DNL Salesforce] à Experience Platform le [!DNL Azure], envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Salesforce] dans le corps de la requête.

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Authentification de base ]

+++Requête

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
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Salesforce] : `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++

+++Réponse

Une réponse réussie renvoie votre nouvelle connexion de base ainsi que son identifiant unique.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB  Informations d’identification du client OAuth 2 ]

+++Requête

La requête suivante crée une connexion de base pour [!DNL Salesforce] à l’aide des informations d’identification du client OAuth 2 :

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
| `auth.params.clientId` | Identifiant client associé à votre compte [!DNL Salesforce]. |
| `auth.params.clientSecret` | Secret client associé à votre compte [!DNL Salesforce]. |
| `auth.params.apiVersion` | Version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Salesforce] : `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++


+++Réponse

Une réponse réussie renvoie votre nouvelle connexion de base ainsi que son identifiant unique.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Connexion de [!DNL Salesforce] à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre source [!DNL Salesforce] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Conditions préalables

Pour plus d’informations sur la configuration de votre compte [!DNL Salesforce] pour pouvoir vous connecter à Experience Platform sur AWS, consultez la [[!DNL Salesforce] présentation](../../../../connectors/crm/salesforce.md#aws).

### Créer une connexion de base pour [!DNL Salesforce] sur Experience Platform sur AWS

Pour créer une connexion de base et connecter votre compte [!DNL Salesforce] à Experience Platform sur AWS, envoyez une requête POST au point d’entrée `/connections` et indiquez les valeurs appropriées pour vos informations d’identification.

**Format d’API**

```http
POST /connections
```

**Requête**

+++Sélectionner pour afficher la demande

La requête suivante crée une connexion de base pour la source [!DNL Salesforce] dans Experience Platform sur AWS.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Pour plus d’informations sur la manière de récupérer votre `jwtToken` [!DNL Salesforce], consultez le guide sur [comment configurer une source pour  [!DNL Salesforce]  connecter à Experience Platform sur AWS](../../../../connectors/crm/salesforce.md#aws).

+++

**Réponse**

+++Sélectionner pour afficher la réponse

Une réponse réussie renvoie votre nouvelle connexion de base ainsi que son identifiant unique.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### Vérification du statut de votre connexion

Pour vérifier le statut de votre connexion, envoyez une requête GET au point d’entrée `/connections` et indiquez l’identifiant de connexion de base qui a été généré à l’étape de création.

**Format d’API**

```http
GET /connections
```

**Requête**

+++Sélectionner pour afficher la demande

La requête suivante récupère des informations pour l’ID de connexion de base : `3e908d3f-c390-482b-9f44-43d3d4f2eb82`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

>[!BEGINTABS]

>[!TAB Initialisation]

+++Sélectionner pour afficher l’exemple de réponse

La réponse suivante affiche des informations pour l’identifiant de connexion de base : `3e908d3f-c390-482b-9f44-43d3d4f2eb82` lorsqu’il est à l’état `initializing`.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB Activé]

+++Sélectionner pour afficher l’exemple de réponse

La réponse suivante affiche des informations pour l’identifiant de connexion de base : `3e908d3f-c390-482b-9f44-43d3d4f2eb82` lorsqu’il est à l’état `enabled`.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Salesforce] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer des données CRM dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/crm.md)
