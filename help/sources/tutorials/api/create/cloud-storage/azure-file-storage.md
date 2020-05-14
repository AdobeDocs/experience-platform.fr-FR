---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur d'Enregistrement de fichiers Azure à l'aide de l'API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 3a882656f93b86093b356be5dbc12b3e4321cfb8
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---


# Création d&#39;un connecteur d&#39;Enregistrement de fichiers Azure à l&#39;aide de l&#39;API Flow Service

>[!NOTE]
>Le connecteur d&#39;Enregistrement de fichiers Azure est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API du service de flux pour vous guider à travers les étapes de connexion de l&#39;Enregistrement de fichiers Azure à la plate-forme d&#39;expérience.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plate-forme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à Azure File Enregistrement à l&#39;aide de l&#39;API Flow Service.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte à l&#39;Enregistrement de fichiers Azure, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point de terminaison de l&#39;instance d&#39;Enregistrement de fichiers Azure à laquelle vous accédez. |
| `userId` | Utilisateur disposant d&#39;un accès suffisant au point de terminaison de l&#39;Enregistrement de fichiers Azure. |
| `password` | Mot de passe de votre instance d&#39;Enregistrement de fichiers Azure |
| ID de spécification de connexion | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour l&#39;Enregistrement de fichier Azure est : `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)d&#39;Enregistrement de fichier Azure.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte d&#39;Enregistrement de fichier Azure, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion d&#39;Enregistrement de fichiers Azure, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande POST. L&#39;ID de spécification de connexion pour l&#39;Enregistrement de fichier Azure est `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`valide.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | Point de terminaison de l&#39;instance d&#39;Enregistrement de fichiers Azure à laquelle vous accédez. |
| `auth.params.userId` | Utilisateur disposant d&#39;un accès suffisant au point de terminaison de l&#39;Enregistrement de fichiers Azure. |
| `auth.params.password` | Clé d&#39;accès d&#39;Enregistrement de fichier Azure. |
| `connectionSpec.id` | ID de spécification de connexion d&#39;Enregistrement de fichier Azure : `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion d&#39;Enregistrement de fichier Azure à l&#39;aide de l&#39;API Flow Service et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer un enregistrement cloud tiers à l’aide de l’API](../../explore/cloud-storage.md)de service de flux.
