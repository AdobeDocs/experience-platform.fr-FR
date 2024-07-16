---
keywords: Experience Platform;accueil;rubriques populaires;Data Explorer Azure;Data Explorer Azure;Data Explorer Azure
solution: Experience Platform
title: Création d’une connexion de base de Data Explorer Azure à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Azure Data Explorer à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 62%

---

# Créez une connexion de base [!DNL Azure Azure Data Explorer] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Azure Data Explorer] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Azure Data Explorer] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Azure Data Explorer], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Point d’entrée du serveur [!DNL Azure Data Explorer]. |
| `database` | Nom de la base de données [!DNL Azure Data Explorer]. |
| `tenant` | L’identifiant de tenant unique utilisé pour se connecter à la base de données [!DNL Azure Data Explorer]. |
| `servicePrincipalId` | L’identifiant principal de service unique utilisé pour se connecter à la base de données [!DNL Azure Data Explorer]. |
| `servicePrincipalKey` | Clé principale de service unique utilisée pour la connexion à la base de données [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’ID de spécification de connexion pour [!DNL Azure Data Explorer] est `0479cc14-7651-4354-b233-7480606c2ac3`. |

Pour plus d&#39;informations sur la prise en main, consultez ce [[!DNL Azure Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Azure Data Explorer] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Azure Data Explorer] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.endpoint` | Point d’entrée du serveur [!DNL Azure Data Explorer]. |
| `auth.params.database` | Nom de la base de données [!DNL Azure Data Explorer]. |
| `auth.params.tenant` | L’identifiant de tenant unique utilisé pour se connecter à la base de données [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalId` | L’identifiant principal de service unique utilisé pour se connecter à la base de données [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalKey` | Clé principale de service unique utilisée pour la connexion à la base de données [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Azure Data Explorer] : `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base [!DNL Azure Data Explorer] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
