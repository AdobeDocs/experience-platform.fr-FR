---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur Oracle à l’aide de l’API Flow Service
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---


# Création d’un [!DNL Oracle] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>Le [!DNL Oracle] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates au sein de l’Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider à travers les étapes de la connexion [!DNL Oracle] à [!DNL Experience Platform].

## Prise en main

Ce guide exige une compréhension pratique des éléments suivants de l&#39;Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Oracle] l’aide de l’ [!DNL Flow Service] API.

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour la connexion à [!DNL Oracle]. Le modèle de chaîne de [!DNL Oracle] connexion est le suivant : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Oracle] est `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ce document](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199)Oracle.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de [!DNL Experience Platform] dépannage.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux [!DNL Platform] API, vous devez d&#39;abord suivre le didacticiel [d&#39;](../../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’ [!DNL Experience Platform] API, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux [!DNL Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Un seul connecteur est nécessaire par [!DNL Oracle] compte, car il peut être utilisé pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une [!DNL Oracle] connexion, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande POST. L&#39;ID de spécification de connexion pour [!DNL Oracle] est `d6b52d86-f0f8-475f-89d4-ce54c8527328`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle connection",
        "description": "A connection for Oracle",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                    "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à votre [!DNL Oracle] base de données. Le modèle de chaîne de [!DNL Oracle] connexion est le suivant : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | ID de spécification de [!DNL Oracle] connexion : `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL Oracle] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API](../../explore/database-nosql.md)Flow Service.
