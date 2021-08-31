---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google PubSub;google pubsub
solution: Experience Platform
title: Création d’une connexion Google PubSub-Source à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un compte Google PubSub à l’aide de l’API Flow Service.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 7%

---

# Création d’une connexion source [!DNL Google PubSub] à l’aide de l’API Flow Service

>[!NOTE]
>
>Le connecteur [!DNL Google PubSub] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Ce tutoriel vous guide tout au long des étapes permettant de connecter [!DNL Google PubSub] (ci-après appelé &quot;[!DNL PubSub]&quot;) à l’Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour connecter [!DNL PubSub] à Platform à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL PubSub], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `projectId` | ID de projet requis pour l’authentification [!DNL PubSub]. |
| `credentials` | Informations d’identification ou clé requises pour l’authentification [!DNL PubSub]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions cible de base et source. L’identifiant de spécification de connexion [!DNL PubSub] est : `70116022-a743-464a-bbfe-e226a7f8210c`. |

Pour plus d’informations sur ces valeurs, consultez ce document [[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication) . Pour utiliser l’authentification par compte de service, consultez ce [[!DNL PubSub] guide sur la création de comptes de service](https://cloud.google.com/docs/authentication/production#create_service_account) pour connaître les étapes de génération de vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

La première étape de la création d’une connexion source consiste à authentifier votre source [!DNL PubSub] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL PubSub] dans le cadre des paramètres de requête.

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
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.projectId` | ID de projet requis pour l’authentification [!DNL PubSub]. |
| `auth.params.credentials` | Informations d’identification ou clé requises pour l’authentification [!DNL PubSub]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL PubSub] : `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion, y compris son identifiant unique (`id`). Cet identifiant de connexion de base est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Création d’une connexion source {#source}

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et un identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation IMS.

Pour créer une connexion source, envoyez une requête de POST au point de terminaison `/sourceConnections` de l’API [!DNL Flow Service].

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez fournir pour inclure plus d’informations sur votre connexion source. |
| `baseConnectionId` | L’identifiant de connexion de base de votre source [!DNL PubSub] qui a été généré à l’étape précédente. |
| `connectionSpec.id` | L’identifiant de spécification de connexion fixe pour [!DNL PubSub]. Cet identifiant est : `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Format des données [!DNL PubSub] que vous souhaitez ingérer. Actuellement, le seul format de données pris en charge est `json`. |
| `params.topicId` | L’ID de rubrique définit la ressource nommée spécifique qui les messages sont envoyés par les éditeurs. |
| `params.subscriptionId` | L’ID d’abonnement définit la ressource nommée spécifique qui représente le flux de messages d’une seule rubrique spécifique à diffuser à l’application d’abonnement. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis dans le tutoriel suivant pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion source [!DNL PubSub] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’ [!DNL Flow Service] API](../../collect/streaming.md).
