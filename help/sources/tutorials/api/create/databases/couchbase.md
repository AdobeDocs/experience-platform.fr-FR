---
keywords: Experience Platform;accueil;rubriques les plus consultées;couchbase;Couchbase
solution: Experience Platform
title: Création d’une connexion de base Couchbase à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Couchbase à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 625e3acf-fc27-44cf-b4e6-becf1d107ff2
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 63%

---

# Créez une connexion de base à [!DNL Couchbase] à l’aide de l’API [!DNL Flow Service].

>[!NOTE]
>
>Le [!DNL Couchbase] Le connecteur est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs libellés en version bêta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Couchbase] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Couchbase] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Couchbase] instance. Le modèle de chaîne de connexion pour [!DNL Couchbase] is `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Pour plus d’informations sur l’acquisition d’une chaîne de connexion, reportez-vous à la section [ce document Couchbase](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Couchbase] is `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Couchbase] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Couchbase] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à un [!DNL Couchbase] compte . Le modèle de chaîne de connexion est le suivant : `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. |
| `connectionSpec.id` | Le [!DNL Couchbase] identifiant de spécification de connexion : `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Couchbase] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/database-nosql.md)
