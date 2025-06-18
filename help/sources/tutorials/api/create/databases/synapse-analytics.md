---
title: Connecter Azure Synapse Analytics à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter votre compte Azure Synapse Analytics à Experience Platform à l’aide d’API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 15%

---

# Connexion de [!DNL Azure Synapse Analytics] à Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>La source [!DNL Azure Synapse Analytics] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Azure Synapse Analytics] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Azure Synapse Analytics] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez la [[!DNL Azure Synapse Analytics] présentation](../../../../connectors/databases/synapse-analytics.md#prerequisites) pour plus d’informations sur l’authentification.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Connexion de [!DNL Azure Synapse Analytics] à Experience Platform

Lisez ce qui suit pour savoir comment créer une connexion de base et connecter votre compte [!DNL Azure Synapse Analytics] à Experience Platform.

### Créer une connexion de base

Une **connexion de base** stocke des informations essentielles qui relient votre système source à Adobe Experience Platform. Cela inclut :

* Les informations d’authentification de votre source
* Statut actuel de la connexion
* Un **identifiant de connexion de base** unique

L’**identifiant de connexion de base** vous permet de parcourir et d’explorer les fichiers de votre source, ce qui vous permet d’identifier les éléments à ingérer, ainsi que leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections`, y compris vos informations d’authentification [!DNL Azure Synapse Analytics] dans les paramètres de requête.

**Format d’API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Authentification basée sur une chaîne de connexion]

**Requête**

La requête suivante crée une connexion de base pour [!DNL Azure Synapse Analytics] à l’aide de l’authentification par chaîne de connexion.

+++Afficher un exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à [!DNL Azure Synapse Analytics]. Le modèle de chaîne de connexion [!DNL Azure Synapse Analytics] est `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Azure Synapse Analytics] est : `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB Authentification basée sur la clé principale du service]

La requête suivante crée une connexion de base pour [!DNL Azure Synapse Analytics] à l’aide de l’authentification par clé de service principale.

**Requête**

+++Afficher un exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Informations d’identification | Description |
| --- | --- |
| `auth.params.server` | Nom de domaine complet de votre point d’entrée SQL [!DNL Azure Synapse Analytics]. |
| `auth.params.database` | Nom de la base de données spécifique dans votre espace de travail [!DNL Azure Synapse Analytics]. |
| `auth.params.tenant` | Identifiant client [!DNL Azure Active Directory] associé à votre abonnement [!DNL Azure]. |
| `auth.params.servicePrincipalId` | Identifiant client d’une application [!DNL Azure Active Directory]. |
| `auth.params.servicePrincipalKey` | Secret client ou mot de passe associé au principal de service. |
| `connectSpec.id` | Identifiant de spécification de connexion de [!DNL Azure Synapse Analytics]. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Azure Synapse Analytics] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
