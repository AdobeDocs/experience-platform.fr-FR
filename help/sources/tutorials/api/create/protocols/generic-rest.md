---
keywords: Experience Platform;accueil;rubriques populaires;REST générique;repos générique
solution: Experience Platform
title: Création d’une connexion de base d’API REST générique à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter l’API REST générique à Adobe Experience Platform à l’aide de l’API Flow Service.
source-git-commit: 1a9c4d5ba3ba9201378e78c0e92dea5101668a24
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 6%

---

# Créez une connexion de base d’API REST générique à l’aide du [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Generic REST API] La source est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs bêta-étiquetés.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Generic REST API] en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../../../landing/api-guide.md).

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Generic REST API], vous devez fournir des informations d’identification valides pour le type d’authentification de votre choix. [!DNL Generic REST API] prend en charge le code d’actualisation OAuth 2 et l’authentification de base. Consultez les tableaux suivants pour plus d’informations sur les informations d’identification des deux types d’authentification pris en charge.

#### Code d’actualisation OAuth 2

| Credential | Description |
| --- | --- |
| `host` | URL d’hôte de la source à laquelle vous effectuez votre demande. Cette valeur est requise et ne peut pas être ignorée à l’aide de `requestParameterOverride`. |
| `authorizationTestUrl` | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |
| `clientId` | (Facultatif) Identifiant client associé à votre compte utilisateur. |
| `clientSecret` | (Facultatif) Le secret client associé à votre compte utilisateur. |
| `accessToken` | Informations d’identification d’authentification Principales utilisées pour accéder à votre application. Le jeton d’accès représente l’autorisation de votre application, pour accéder à certains aspects des données d’un utilisateur. Cette valeur est requise et ne peut pas être ignorée à l’aide de `requestParameterOverride`. |
| `refreshToken` | (Facultatif) Jeton utilisé pour générer un nouveau jeton d’accès, lorsque le jeton d’accès a expiré. |
| `expirationDate` | (Facultatif) Une valeur masquée qui définit la date d’expiration de votre jeton d’accès. |
| `accessTokenUrl` | (Facultatif) Le point de terminaison URL utilisé pour récupérer votre jeton d’accès. |
| `requestParameterOverride` | (Facultatif) Une propriété qui vous permet de spécifier les paramètres d’identification à remplacer. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Generic REST API] est : `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Authentification de base

| Credential | Description |
| --- | --- |
| `host` | URL d’hôte de la source à laquelle vous effectuez votre demande. |
| `username` | Nom d’utilisateur correspondant à votre compte d’utilisateur. |
| `password` | Mot de passe correspondant à votre compte utilisateur. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Generic REST API] est : `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

[!DNL Generic REST API] prend en charge l’authentification de base et le code d’actualisation OAuth 2. Consultez les exemples suivants pour savoir comment vous authentifier avec l’un ou l’autre des types d’authentification.

### Créez un [!DNL Generic REST API] connexion de base à l’aide du code d’actualisation OAuth 2

Pour créer un identifiant de connexion de base à l’aide du code d’actualisation OAuth 2, envoyez une requête de POST au `/connections` point de terminaison tout en fournissant vos informations d’identification OAuth 2.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion de base. |
| `description` | (Facultatif) Une propriété que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | L’identifiant de spécification de connexion associé à [!DNL Generic REST API]. Cet ID fixe est : `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Type d’authentification que vous utilisez pour authentifier votre source sur Platform. |
| `auth.params.host` | L’URL racine utilisée pour se connecter à votre [!DNL Generic REST API] source. |
| `auth.params.accessToken` | Jeton d’accès correspondant utilisé pour authentifier votre source. Ceci est requis pour l’authentification basée sur OAuth. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Créez un [!DNL Generic REST API] connexion de base à l’aide de l’authentification de base

Pour créer une [!DNL Generic REST API] connexion de base à l’aide de l’authentification de base, effectuez une requête de POST à l’adresse `/connections` point d’entrée [!DNL Flow Service] API lors de la fourniture de vos informations d’authentification de base.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion de base. |
| `description` | (Facultatif) Une propriété que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | L’identifiant de spécification de connexion associé à [!DNL Generic REST API]. Cet ID fixe est : `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Type d’authentification que vous utilisez pour connecter votre source à Platform. |
| `auth.params.host` | L’URL racine utilisée pour se connecter à votre [!DNL Generic REST API] source. |
| `auth.params.username` | Le nom d’utilisateur correspondant à votre [!DNL Generic REST API] source. Ceci est requis pour l’authentification de base. |
| `auth.params.password` | Le mot de passe qui correspond à votre [!DNL Generic REST API] source. Ceci est requis pour l’authentification de base. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer la structure de fichiers et le contenu de votre source à l’étape suivante.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Generic REST API] connexion à l’aide de la fonction [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [exploration des applications de protocoles à l’aide de l’API Flow Service ;](../../explore/protocols.md).
