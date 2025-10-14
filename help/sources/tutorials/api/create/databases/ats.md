---
keywords: Experience Platform;accueil;rubriques populaires;[!DNL Azure Table Storage];[!DNL Azure Table Storage];Stockage de table Azure
solution: Experience Platform
title: Créer une connexion de base de stockage de table Azure à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Azure Table Storage à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 54%

---

# Créer une connexion de base [!DNL Azure Table Storage] à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le connecteur [!DNL Azure Table Storage] est en version bêta. Consultez la [&#x200B; Présentation des sources &#x200B;](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Azure Table Storage] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Azure Table Storage] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Azure Table Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour la connexion à une instance [!DNL Azure Table Storage]. Le modèle de chaîne de connexion pour [!DNL Azure Table Storage] est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Azure Table Storage] est `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

Pour plus d&#39;informations sur l&#39;obtention d&#39;une chaîne de connexion, consultez [ce [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Azure Table Storage] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Azure Table Storage] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à une instance [!DNL Azure Table Storage]. Le modèle de chaîne de connexion pour [!DNL Azure Table Storage] est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Azure Table Storage] : `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base [!DNL Azure Table Storage] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
