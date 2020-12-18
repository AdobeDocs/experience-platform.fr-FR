---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Création d’un connecteur Microsoft Dynamics à l’aide de l’API du service de flux
topic: overview
type: Tutorial
description: Ce didacticiel utilise l'API Flow Service pour vous guider à travers les étapes de connexion de Platform à un compte Microsoft Dynamics (ci-après appelé "Dynamics") pour la collecte de données de gestion de la relation client.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 26%

---


# Créez un connecteur [!DNL Microsoft Dynamics] à l’aide de l’API [!DNL Flow Service].

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de connexion de [!DNL Platform] à un compte [!DNL Microsoft Dynamics] (ci-après appelé &quot;Dynamics&quot;) pour la collecte de données de gestion de la relation client.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL xperience Platform] Efournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir connecter [!DNL Platform] à un compte Dynamics à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Dynamics], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUri` | URL de service de votre instance [!DNL Dynamics]. |
| `username` | Nom d’utilisateur de votre compte d’utilisateur [!DNL Dynamics]. |
| `password` | Mot de passe de votre compte [!DNL Dynamics]. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document Dynamics](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](../../../../../tutorials/authentication.md). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL Dynamics], car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL Dynamics], l&#39;identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL Dynamics] est `38ad80fe-8b06-4938-94f4-d4ee80266b07`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics Connection",
        "description": "connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUri` | URI de service associé à votre instance [!DNL Dynamics]. |
| `auth.params.username` | Nom d&#39;utilisateur associé à votre compte [!DNL Dynamics]. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Dynamics]. |
| `connectionSpec.id` | Spécification de connexion `id` de votre compte [!DNL Dynamics] récupérée à l&#39;étape précédente. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre système de gestion de la relation client à l’étape suivante.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL Dynamics] à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer les systèmes de gestion de la relation client à l’aide de l’API Flow Service](../../explore/crm.md).