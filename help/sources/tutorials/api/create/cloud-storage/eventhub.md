---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur Azure Événement Hubs à l'aide de l'API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: 11431ffcfc2204931fe3e863bfadc7878a40b49c
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---


# Création d’un [!DNL Azure Event Hubs] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
> Le [!DNL Azure Event Hubs] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates au sein de l’Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider dans les étapes de la connexion [!DNL Experience Platform] à un [!DNL Azure Event Hubs] compte.

## Prise en main

Ce guide exige une compréhension pratique des éléments suivants de l&#39;Adobe Experience Platform :

- [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
- [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à un [!DNL Azure Event Hubs] compte à l’aide de l’ [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour pouvoir vous connecter [!DNL Flow Service] à votre [!DNL Azure Event Hubs] compte, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `sasKeyName` | Nom de la règle d&#39;autorisation, également connue sous le nom de clé SAS. |
| `sasKey` | Signature d’accès partagé générée. |
| `namespace` | L&#39;espace de nommage des Événements Hubs auxquels vous accédez. |
| `connectionSpec.id` | ID de spécification de [!DNL Azure Event Hubs] connexion : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Événement Hubs.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de [!DNL Experience Platform] dépannage.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux [!DNL Platform] API, vous devez d&#39;abord suivre le didacticiel [d&#39;](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’ [!DNL Experience Platform] API, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux [!DNL Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

- Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par [!DNL Azure Event Hubs] compte, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Basic Authentication for Event Hubs",
            "params": {
                "sasKeyName": "sasKeyName",
                "sasKey": "sasKey",
                "namespace": "namespace"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.sasKeyName` | Nom de la règle d&#39;autorisation, également connue sous le nom de clé SAS. |
| `auth.params.sasKey` | Signature d’accès partagé générée. |
| `namespace` | espace de nommage de l’ [!DNL Event Hubs] accès auquel vous accédez. |
| `connectionSpec.id` | ID de spécification de [!DNL Azure Event Hubs] connexion : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données d’enregistrement de cloud dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL Azure Event Hubs] connexion à l’aide d’API et un identifiant unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet ID de connexion pour [explorer les enregistrements du cloud à l’aide de l’API](../../explore/cloud-storage.md)de service de flux.