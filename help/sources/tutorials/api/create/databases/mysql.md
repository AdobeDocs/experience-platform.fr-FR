---
keywords: Experience Platform;accueil;rubriques les plus consultées;MySQL;mysql
solution: Experience Platform
title: Création d’une [!DNL MySQL] connexion de base à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à MySQL à l’aide de l’API Flow Service.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 12%

---

# Créez une connexion de base [!DNL MySQL] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL MySQL] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL MySQL] à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à votre stockage [!DNL MySQL], vous devez fournir la valeur de la propriété de connexion suivante :

| Credential | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion [!DNL MySQL] associée à votre compte. Le modèle de chaîne de connexion [!DNL MySQL] est le suivant : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL MySQL] est `26d738e0-8963-47ea-aadf-c60de735468a`. |

Pour plus d’informations sur l’obtention d’une chaîne de connexion, consultez ce [[!DNL MySQL] document](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL MySQL] dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL MySQL] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL MySQL] Test Connection",
        "description": "[!DNL MySQL] Test Connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion [!DNL MySQL] associée à votre compte. Le modèle de chaîne de connexion [!DNL MySQL] est le suivant : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL MySQL] : `26d738e0-8963-47ea-aadf-c60de735468a`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre base de données dans le tutoriel suivant.

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL MySQL] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion dans le tutoriel suivant lorsque vous apprendrez à [explorer des bases de données ou des systèmes NoSQL à l’aide de l’API Flow Service](../../explore/database-nosql.md).
