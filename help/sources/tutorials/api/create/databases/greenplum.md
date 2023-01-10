---
keywords: Experience Platform;accueil;rubriques les plus consultées;greenplum;Greenplum
solution: Experience Platform
title: Création d’une connexion de base GreenPlum à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter GreenPlum à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: c4ce452a-b4c5-46ab-83ab-61b296c271d0
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 65%

---

# Créez une connexion de base à [!DNL GreenPlum] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL GreenPlum] à l’aide de l’[[!DNL Flow Service] API](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL GreenPlum] en utilisant la variable [!DNL Flow Service] API.

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL GreenPlum] instance. Le modèle de chaîne de connexion pour [!DNL GreenPlum] is `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL GreenPlum] is `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

Pour plus d’informations sur l’acquisition d’une chaîne de connexion, reportez-vous à la section [ce document GreenPlum ;](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL GreenPlum] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL GreenPlum] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "GreenPlum test connection",
        "description": "A test connection for a GreenPlum source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "connectionString": "HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "37b6bf40-d318-4655-90be-5cd6f65d334b",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à un [!DNL GreenPlum] compte . Le modèle de chaîne de connexion est le suivant : `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Le [!DNL GreenPlum] identifiant de spécification de connexion : `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL GreenPlum] connexion de base à l’aide de [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/database-nosql.md)
