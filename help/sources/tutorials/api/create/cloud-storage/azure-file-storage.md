---
keywords: Experience Platform;accueil;rubriques populaires;Azure;Stockage de fichiers Azure;Stockage de fichiers Azure
solution: Experience Platform
title: Créer une connexion de base Azure File Storage à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Azure File Storage à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 51%

---

# Créer une connexion de base [!DNL Azure File Storage] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Azure File Storage] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Azure File Storage] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Azure File Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point d’entrée de l’instance [!DNL Azure File Storag]e à laquelle vous accédez. |
| `userId` | L’utilisateur disposant d’un accès suffisant au point d’entrée [!DNL Azure File Storage]. |
| `password` | Mot de passe de votre instance [!DNL Azure File Storage] |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Azure File Storage] est `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Pour plus d’informations sur la prise en main, consultez [ce document Azure File Storage](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Azure File Storage] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Azure File Storage] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | Point d’entrée de l’instance [!DNL Azure File Storage] à laquelle vous accédez. |
| `auth.params.userId` | L’utilisateur disposant d’un accès suffisant au point d’entrée [!DNL Azure File Storage]. |
| `auth.params.password` | La clé d’accès [!DNL Azure File Storage]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Azure File Storage] : `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion [!DNL Azure File Storage] à l’aide de l’API [!DNL Flow Service] et d’obtenir la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer un stockage cloud tiers à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
