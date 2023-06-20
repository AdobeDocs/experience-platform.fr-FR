---
title: Création d’une connexion de base de Snowflake à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Snowflake à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 47%

---

# Créez une connexion de base à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service].

>[!IMPORTANT]
>
>Le [!DNL Snowflake] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Snowflake] à l’aide de l’[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Snowflake] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `account` | Le nom complet du compte associé à votre [!DNL Snowflake] compte . Une personne entièrement qualifiée [!DNL Snowflake] nom du compte inclut le nom de votre compte, votre région et votre plateforme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d&#39;informations sur les noms de compte, reportez-vous à cette section [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | Le [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| `database` | Le [!DNL Snowflake] La base de données contient les données que vous souhaitez importer dans Platform. |
| `username` | Nom d’utilisateur de la variable [!DNL Snowflake] compte . |
| `password` | Le mot de passe du [!DNL Snowflake] compte utilisateur. |
| `role` | Le rôle de contrôle d’accès par défaut à utiliser dans la variable [!DNL Snowflake] session. Le rôle doit être un rôle existant qui a déjà été attribué à l’utilisateur spécifié. Le rôle par défaut est `PUBLIC`. |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Snowflake] is `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Snowflake] document](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>Vous devez définir la variable `PREVENT_UNLOAD_TO_INLINE_URL` indicateur pour `FALSE` pour permettre le déchargement des données de votre [!DNL Snowflake] base de données vers Experience Platform.

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Snowflake] informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Snowflake] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Le [!DNL Snowflake] identifiant de spécification de connexion : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de , y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/database-nosql.md)
