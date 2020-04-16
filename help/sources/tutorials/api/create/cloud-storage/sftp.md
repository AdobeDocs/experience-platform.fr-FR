---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur SFTP à l’aide de l’API du service de flux
topic: overview
translation-type: tm+mt
source-git-commit: a038abcdc411b638f41b94dea0140518c12f5600

---


# Création d’un connecteur SFTP à l’aide de l’API du service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API du service de flux pour vous guider tout au long des étapes nécessaires à la connexion de la plate-forme d’expérience à un serveur SFTP (Secure File Transfer Protocol).

Si vous préférez utiliser l’interface utilisateur dans la plateforme d’expérience, le didacticiel [de l’](../../../ui/create/cloud-storage/ftp-sftp.md) interface utilisateur fournit des instructions étape par étape pour exécuter des actions similaires.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à un serveur SFTP à l’aide de l’API de service de flux.

### Collecte des informations d’identification requises

Pour que le service de flux se connecte au SFTP, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Nom ou adresse IP associé à votre serveur SFTP. |
| `username` | Nom d’utilisateur ayant accès à votre serveur SFTP. |
| `password` | mot de passe de votre serveur SFTP. |

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../../../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type : `application/json`

## Rechercher les spécifications de connexion

Pour créer une connexion SFTP, un ensemble de spécifications de connexion SFTP doit exister dans le service de flux. La première étape de la connexion de Platform à SFTP consiste à récupérer ces spécifications.

**Format API**

Chaque source disponible possède son propre jeu de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d’authentification. Vous pouvez rechercher les spécifications de connexion pour SFTP en exécutant une requête GET et en utilisant des paramètres de .

L&#39;envoi d&#39;une requête GET sans paramètres  retournera les spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure le `property=name=="sftp"` pour obtenir des informations spécifiques pour SFTP.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="sftp"
```

**Requête**

La requête suivante récupère les spécifications de connexion d’un serveur SFTP.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="sftp"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la spécification de connexion du serveur SFTP, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "name": "sftp",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for sftp",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to sftp",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specify the name or IP address of the SFTP server."
                            },
                            "userName": {
                                "type": "string",
                                "description": "Specify the user who has access to the SFTP server."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the password for the user (userName).",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userName",
                            "password"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Créer une connexion de base

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par compte SFTP, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "password": "{PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.host` | Nom d’hôte de votre serveur SFTP. |
| `auth.params.username` | Nom d’utilisateur associé à votre serveur SFTP. |
| `auth.params.password` | mot de passe associé à votre serveur SFTP. |
| `connectionSpec.id` | Spécification `id` de connexion de votre serveur SFTP récupérée à l’étape précédente. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion de base nouvellement créée. Cet identifiant est nécessaire pour explorer votre serveur SFTP dans le didacticiel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion SFTP à l’aide de l’API du service de flux et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet ID de connexion pour [explorer  cloud à l’aide de l’API](../../explore/cloud-storage.md) de service de flux ou [assimiler des données de parquet à l’aide de l’API](../../cloud-storage-parquet.md)de service de flux.
