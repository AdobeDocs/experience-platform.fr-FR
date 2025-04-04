---
keywords: Experience Platform;accueil;rubriques populaires;Azure Data Lake Storage Gen2;stockage azure data lake;Azure
solution: Experience Platform
title: Créer une connexion de base Azure Data Lake Storage Gen2 à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Azure Data Lake Storage Gen2 à l’aide de l’API Flow Service.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 30%

---

# Créer une connexion de base [!DNL Azure Data Lake Storage Gen2] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion de base pour [!DNL Azure Data Lake Storage Gen2] (ci-après dénommée « ADLS Gen2 ») à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance d’Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir la création d’une connexion source ADLS Gen2 à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puissiez vous connecter à ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | Point d’entrée pour ADLS Gen2. Le modèle de point d’entrée est le suivant : `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | Identifiant client de l’application. |
| `servicePrincipalKey` | Clé de l’application. |
| `tenant` | Informations sur le client qui contient votre application. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour ADLS Gen2 est : `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Pour plus d’informations sur ces valeurs, consultez [ce document ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification ADLS Gen2 dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour ADLS Gen2 :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.url` | Point d’entrée de l’URL de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalId` | Identifiant principal de service de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Clé principale de service de votre compte ADLS Gen2. |
| `auth.params.tenant` | Informations sur le client de votre compte ADLS Gen2. |
| `connectionSpec.id` | Identifiant de spécification de connexion ADLS Gen2 : `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion ADLS Gen2 à l’aide d’API et obtenu un identifiant unique dans le cadre du corps de la réponse. Vous pouvez utiliser cet identifiant de connexion pour [explorer les espaces de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
