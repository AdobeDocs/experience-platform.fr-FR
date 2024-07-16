---
keywords: Experience Platform;accueil;rubriques populaires;REST générique;repos générique
solution: Experience Platform
title: Création d’une connexion de base d’API REST générique à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter l’API REST générique à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 58%

---

# Créez une connexion de base d’API REST générique à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>La source [!DNL Generic REST API] est en version Beta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Generic REST API] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Generic REST API], vous devez fournir des informations d’identification valides pour le type d’authentification de votre choix. [!DNL Generic REST API] prend en charge le code d’actualisation OAuth 2 et l’authentification de base. Consultez les tableaux suivants pour plus d’informations sur les informations d’identification des deux types d’authentification pris en charge.

#### Code d’actualisation OAuth 2

| Informations d’identification | Description |
| --- | --- |
| `host` | URL de l’hôte de la source à laquelle vous effectuez votre demande. Cette valeur est requise et ne peut pas être ignorée à l’aide de `requestParameterOverride`. |
| `authorizationTestUrl` | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |
| `clientId` | (Facultatif) Identifiant client associé à votre compte utilisateur. |
| `clientSecret` | (Facultatif) Le secret client associé à votre compte utilisateur. |
| `accessToken` | Informations d’identification d’authentification principales utilisées pour accéder à votre application. Le jeton d’accès représente l’autorisation de votre application, pour accéder à certains aspects des données d’un utilisateur. Cette valeur est requise et ne peut pas être ignorée à l’aide de `requestParameterOverride`. |
| `refreshToken` | (Facultatif) Jeton utilisé pour générer un nouveau jeton d’accès, lorsque le jeton d’accès a expiré. |
| `expirationDate` | (Facultatif) Une valeur masquée qui définit la date d’expiration de votre jeton d’accès. |
| `accessTokenUrl` | (Facultatif) Le point de terminaison URL utilisé pour récupérer votre jeton d’accès. |
| `requestParameterOverride` | (Facultatif) Une propriété qui vous permet de spécifier les paramètres d’identification à remplacer. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Generic REST API] est `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Authentification de base

| Informations d’identification | Description |
| --- | --- |
| `host` | URL de l’hôte de la source à laquelle vous effectuez votre demande. |
| `username` | Nom d’utilisateur correspondant à votre compte d’utilisateur. |
| `password` | Mot de passe correspondant à votre compte utilisateur. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Generic REST API] est `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

[!DNL Generic REST API] prend en charge l’authentification de base et le code d’actualisation OAuth 2. Consultez les exemples suivants pour savoir comment vous authentifier avec l’un ou l’autre de ces types d’authentification.

### Créer une connexion de base [!DNL Generic REST API] à l’aide du code d’actualisation OAuth 2

Pour créer un identifiant de connexion de base à l’aide du code d’actualisation OAuth 2, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’identification OAuth 2.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Generic REST API] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Propriété | Description |
| --------- | ----------- |
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est explicite, car vous pouvez lʼutiliser pour rechercher des informations sur votre connexion de base. |
| `description` | (Facultatif) Propriété que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | L’identifiant de spécification de connexion associé à [!DNL Generic REST API]. Cet ID fixe est `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Type d’authentification que vous utilisez pour authentifier votre source sur Platform. |
| `auth.params.host` | URL racine utilisée pour se connecter à la source [!DNL Generic REST API]. |
| `auth.params.accessToken` | Jeton d’accès correspondant utilisé pour authentifier la source. Ceci est requis pour l’authentification basée sur OAuth. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Créer une connexion de base [!DNL Generic REST API] à l’aide de l’authentification de base

Pour créer une connexion de base [!DNL Generic REST API] à l’aide de l’authentification de base, envoyez une requête de POST au point de terminaison `/connections` de l’API [!DNL Flow Service] tout en fournissant vos informations d’authentification de base.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Generic REST API] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est explicite, car vous pouvez lʼutiliser pour rechercher des informations sur votre connexion de base. |
| `description` | (Facultatif) Propriété que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | L’identifiant de spécification de connexion associé à [!DNL Generic REST API]. Cet ID fixe est `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Type d’authentification que vous utilisez pour connecter votre source à Platform. |
| `auth.params.host` | URL racine utilisée pour se connecter à la source [!DNL Generic REST API]. |
| `auth.params.username` | Nom d’utilisateur correspondant à votre source [!DNL Generic REST API]. Ceci est requis pour l’authentification de base. |
| `auth.params.password` | Mot de passe correspondant à votre source [!DNL Generic REST API]. Ceci est requis pour l’authentification de base. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer la structure de fichiers et le contenu de votre source à l’étape suivante.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Generic REST API] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de protocoles à Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/protocols.md)
