---
title: Connecter Salesforce Marketing Cloud à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter votre compte Salesforce Marketing Cloud à Experience Platform à l’aide d’API.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 6%

---

# Connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!WARNING]
>
>La source [!DNL Salesforce Marketing Cloud] sera abandonnée en janvier 2026. Une nouvelle source sera publiée plus tard cette année comme alternative. Une fois la nouvelle source publiée, vous devez planifier la migration vers la nouvelle source en créant de nouvelles connexions de compte et de nouveaux flux de données avant la fin du mois de janvier 2026.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Salesforce Marketing Cloud] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Azure Synapse Analytics] à l’aide de l’API [!DNL Flow Service].


### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Salesforce Marketing Cloud] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez la [[!DNL Salesforce Marketing Cloud] présentation de l’authentification](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md) pour plus d’informations sur l’authentification.

### Utilisation des API Experience Platform

Lisez le guide sur [Prise en main des API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

## Connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform sur [!DNL Azure]

Lisez ce qui suit pour savoir comment créer une connexion de base et connecter votre compte [!DNL Salesforce Marketing Cloud] à Experience Platform sur [!DNL Azure].

### Créer une connexion de base {#azure-base}

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par l’intégration source [!DNL Salesforce Marketing Cloud].

Une **connexion de base** stocke des informations essentielles qui relient votre système source à Adobe Experience Platform. Cela inclut :

* Les informations d’authentification de votre source
* Statut actuel de la connexion
* Un **identifiant de connexion de base** unique

L’**identifiant de connexion de base** vous permet de parcourir et d’explorer les fichiers de votre source, ce qui vous permet d’identifier les éléments à ingérer, ainsi que leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections`, y compris vos informations d’authentification [!DNL Salesforce Marketing Cloud] dans les paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Salesforce Marketing Cloud].

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
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.host` |
| `auth.params.clientId` | Identifiant client associé à votre application [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | Secret client associé à votre application [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Salesforce Marketing Cloud] : `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++Afficher l’exemple de réponse

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre compte [!DNL Salesforce Marketing Cloud] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base {#aws-base}

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Salesforce Service Cloud] connecter à Experience Platform sur AWS.

+++Afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Créer un flux de données pour les données [!DNL Salesforce Marketing Cloud]

Maintenant que vous avez correctement connecté votre compte [!DNL Salesforce Marketing Cloud], vous pouvez [créer un flux de données et ingérer les données de votre fournisseur d’automatisation marketing dans Experience Platform](../../collect/marketing-automation.md).