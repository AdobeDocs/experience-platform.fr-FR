---
keywords: Experience Platform;accueil;rubriques les plus consultées;Salesforce Service Cloud;Salesforce service cloud
solution: Experience Platform
title: Création d’une connexion à la source cloud du service Salesforce à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Salesforce Service Cloud à l’aide de l’API Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 1f13b5fcad683b4c0ede96654e35d6f0c64d9eb7
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 68%

---

# Créez un [!DNL Salesforce Service Cloud] connexion source à l’aide de la fonction [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Salesforce Service Cloud] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Salesforce Service Cloud] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Salesforce Service Cloud], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | ---|
| `environmentUrl` | L’URL de la variable [!DNL Salesforce] instance source. |
| `username` | Le nom d’utilisateur de votre [!DNL Salesforce Service Cloud] compte utilisateur. |
| `password` | Le mot de passe de votre [!DNL Salesforce Service Cloud] compte . |
| `securityToken` | Jeton de sécurité pour votre [!DNL Salesforce Service Cloud] compte . |
| `apiVersion` | (Facultatif) La version de l’API REST de la variable [!DNL Salesforce Service Cloud] que vous utilisez. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce Service Cloud] est `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

Pour plus d’informations sur la prise en main, voir [ce document Salesforce Service Cloud ;](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

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

La requête suivante permet de créer une connexion de base pour [!DNL Salesforce Service Cloud] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for salesforce service cloud",
      "description": "Base connection for salesforce service cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
              "username": "acme-salesforce-service-cloud",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
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

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante. 

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
