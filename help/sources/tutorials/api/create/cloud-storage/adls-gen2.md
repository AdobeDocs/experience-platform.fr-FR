---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur Azure Data Lake   Gen2 à l'aide de l'API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 065076aee83990bcad0110f0d7704a60fac400c6

---


# Création d&#39;un connecteur Azure Data Lake   Gen2 à l&#39;aide de l&#39;API Flow Service

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API Flow Service pour vous guider tout au long des étapes nécessaires pour connecter Experience Platform à Azure Data Lake   Gen2 (ci-après dénommé &quot;ADLS Gen2&quot;).

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plateforme.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir créer un connecteur source ADLS Gen2 à l’aide de l’API du service de flux.

### Collecte des informations d’identification requises

Pour que le service Flow se connecte à ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | URL de l’adresse. |
| `servicePrincipalId` | ID client de l’application. |
| `servicePrincipalKey` | La clé de l&#39;application. |
| `tenant` | Informations sur le client qui contiennent votre application. |

Pour plus d&#39;informations sur ces valeurs, reportez-vous à [cette](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

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

Avant de connecter Platform à ADLS Gen2, vous devez vérifier que les spécifications de connexion existent pour ADLS Gen2. Si les spécifications de connexion n&#39;existent pas, une connexion ne peut pas être établie.

Chaque source disponible possède son propre jeu de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d’authentification. Vous pouvez rechercher les spécifications de connexion pour ADLS Gen2 en exécutant une requête GET et en utilisant des paramètres de .

**Format API**

L&#39;envoi d&#39;une requête GET sans paramètres  retournera les spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure le `property=name=="adls-gen2"` pour obtenir des informations spécifiques pour ADLS Gen2.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="adls-gen2"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour ADLS Gen2.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="adls-gen2"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion pour ADLS Gen2, y compris son identifiant unique (`id`). Cet ID est requis à l’étape suivante pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "name": "adls-gen2",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for adls-gen2",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "properties": {
                            "url": {
                                "type": "string",
                                "description": "Endpoint for Azure Data Lake Storage Gen2."
                            },
                            "servicePrincipalId": {
                                "type": "string",
                                "description": "Service Principal Id to connect to ADLSGen2."
                            },
                            "servicePrincipalKey": {
                                "type": "string",
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "format": "password"
                            },
                            "tenant": {
                                "type": "string",
                                "description": "Tenant information(domain name or tenant ID)."
                            }
                        },
                        "required": [
                            "url",
                            "servicePrincipalId",
                            "servicePrincipalKey",
                            "tenant"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Créer une connexion de base

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base est requise par compte ADLS Gen2, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

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
    -d '{
        "name": "adls-gen2",
        "description": "base connection for adls-gen2",
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
| `auth.params.url` | Point de terminaison de l’URL pour votre compte ADLS Gen2. |
| `auth.params.servicePrincipalId` | ID principal de service de votre compte ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Clé principale de service de votre compte ADLS Gen2. |
| `auth.params.tenant` | Informations sur le locataire de votre compte ADLS Gen2. |
| `connectionSpec.id` | Spécification `id` de connexion de votre compte ADLS Gen2 récupérée à l&#39;étape précédente. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est requis pour explorer votre cloud  à l’étape suivante.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion ADLS Gen2 à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [explorer  cloud à l’aide de l’API](../../explore/cloud-storage.md) de service de flux ou [assimiler des données de parquet à l’aide de l’API](../../cloud-storage-parquet.md)de service de flux.
