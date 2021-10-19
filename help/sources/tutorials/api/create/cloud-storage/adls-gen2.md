---
keywords: Experience Platform ; accueil ; sujets populaires ; Azure Data Lake Storage Gen2 ; stockage de lac de données azure ; Azure Data Lake Storage
solution: Experience Platform
title: Création d'une connexion de base Azure Data Lake Storage Gen2 à l'aide de l'API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Azure Data Lake Storage Gen2 à l’aide de l’API Flow Service.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# Créer un [!DNL Azure Data Lake Storage Gen2] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous explique les étapes à suivre pour créer une connexion de base pour [!DNL Azure Data Lake Storage Gen2] (ci-après dénommés &quot;ADLS Gen2&quot;) utilisant la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une instance de plate-forme unique en environnements virtuels distincts pour aider au développement et à l&#39;évolution d&#39;applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour créer une connexion source ADLS Gen2 à l’aide de la [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| `url` | Point de terminaison pour ADLS Gen2. Le motif de point de terminaison est le suivant : `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | L&#39;ID client de l&#39;application. |
| `servicePrincipalKey` | La clé de l&#39;application. |
| `tenant` | Informations sur le client contenant votre application. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L&#39;ID de spécification de connexion pour ADLS Gen2 est : `0ed90a81-07f4-4586-8190-b40eccef1c5a`. |

Pour plus d’informations sur ces valeurs, voir [ce document ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Utilisation des API de plate-forme

Pour plus d’informations sur la manière d’effectuer des appels vers les API de plate-forme, consultez le guide sur [prise en main des API de plate-forme](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et la plate-forme, y compris les informations d&#39;identification de votre source, l&#39;état actuel de la connexion et votre ID de connexion de base unique. L’ID de connexion de base vous permet d’explorer et de parcourir les fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez assimiler, y compris des informations concernant leurs types et formats de données.

Pour créer un ID de connexion de base, effectuez une demande de POST à l’adresse `/connections` point de terminaison tout en fournissant vos informations d&#39;authentification ADLS Gen2 dans le cadre des paramètres de demande.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour ADLS Gen2 :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.url` | Point de terminaison d’URL de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalId` | ID principal de service de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalKey` | La clé principale de service de votre compte ADLS Gen2. |
| `auth.params.tenant` | Informations sur le client de votre compte ADLS Gen2. |
| `connectionSpec.id` | ID de spécification de connexion ADLS Gen2 : `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion ADLS Gen2 à l’aide d’API et un ID unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [exploration des sites de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
