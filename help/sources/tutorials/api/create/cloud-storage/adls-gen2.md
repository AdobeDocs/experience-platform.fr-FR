---
keywords: Experience Platform;accueil;rubriques populaires;Azure Data Lake Storage Gen2;stockage Azure Data Lake;stockage Azure Data Lake;Azure
solution: Experience Platform
title: Créez une connexion de base Azure Data Lake Storage Gen2 à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Azure Data Lake Storage Gen2 à l’aide de l’API Flow Service.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 41%

---

# Créez une connexion de base [!DNL Azure Data Lake Storage Gen2] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Azure Data Lake Storage Gen2] (ci-après appelée &quot;ADLS Gen2&quot;) à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour créer une connexion source ADLS Gen2 à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | Point de terminaison d’ADLS Gen2. Le modèle de point d’entrée est le suivant : `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | ID client de l’application. |
| `servicePrincipalKey` | Clé de l’application. |
| `tenant` | Les informations du client qui contiennent votre application. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour ADLS Gen2 est : `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification ADLS Gen2 dans le cadre des paramètres de requête.

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
| `auth.params.url` | Point de terminaison URL de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalId` | Identifiant principal de service de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Clé principale de service de votre compte ADLS Gen2. |
| `auth.params.tenant` | Informations du client de votre compte ADLS Gen2. |
| `connectionSpec.id` | ID de spécification de connexion ADLS Gen2 : `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion ADLS Gen2 à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de connexion pour [ explorer le stockage dans le cloud à l’aide de l’API Flow Service ](../../explore/cloud-storage.md).
