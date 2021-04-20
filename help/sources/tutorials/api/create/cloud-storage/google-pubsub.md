---
keywords: Experience Platform ; accueil ; rubriques populaires ; Google PubSub ; google pubsub
solution: Experience Platform
title: Création d’une connexion Google PubSub Source à l’aide de l’API du service de flux
topic: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un compte Google PubSub à l’aide de l’API de service de flux.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 32%

---


# Créer une connexion à la source [!DNL Google PubSub] à l’aide de l’API du service de flux

>[!NOTE]
>
>Le connecteur [!DNL Google PubSub] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Ce didacticiel utilise l&#39;[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) pour vous guider dans les étapes de connexion de [!DNL Google PubSub] (ci-après appelé &quot;[!DNL PubSub]&quot;) à Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour créer une connexion source [!DNL PubSub] à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL PubSub], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `projectId` | ID de projet requis pour authentifier [!DNL PubSub]. |
| `credentials` | Informations d’identification ou clé requises pour authentifier [!DNL PubSub]. |

Pour plus d’informations sur ces valeurs, voir le document [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication) suivant. Si vous utilisez l’authentification basée sur un compte de service, consultez le [Guide PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) suivant pour savoir comment générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification basée sur un compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’aucun espace blanc supplémentaire ne figure dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources en Experience Platform, y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL PubSub], car elle peut être utilisée pour créer plusieurs flux de données afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL PubSub], l&#39;ID de fournisseur et l&#39;ID de spécification de connexion doivent être fournis dans le cadre de la demande de POST. L&#39;ID de fournisseur est `521eee4d-8cbe-4906-bb48-fb6bd4450033` et l&#39;ID de spécification de connexion est `70116022-a743-464a-bbfe-e226a7f8210c`.

**Format d’API**

```http
POST /connections
```

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
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
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
| `auth.params.projectId` | ID de projet requis pour authentifier [!DNL PubSub]. |
| `auth.params.credentials` | Informations d’identification ou clé requises pour authentifier [!DNL PubSub]. |
| `connectionSpec.id` | ID de la spécification de connexion [!DNL PubSub] : `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant de connexion de votre nouvelle connexion [!DNL PubSub]. Cet identifiant est nécessaire pour explorer vos données d’enregistrement de cloud dans le didacticiel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL PubSub] à l&#39;aide de l&#39;API [!DNL Flow Service] et vous avez acquis son identifiant de connexion unique. Vous pouvez utiliser cet ID de connexion pour [collecter des données en flux continu à l’aide de l’API Flow Service](../../collect/streaming.md).
