---
title: Créer une connexion source Google PubSub à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte Google PubSub à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: a826bda356a7205f3d4c0e0836881530dbaaf54e
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 59%

---

# Créer une connexion source [!DNL Google PubSub] à l’aide de l’API Flow Service

>[!IMPORTANT]
>
>La variable [!DNL Google PubSub] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Ce tutoriel vous guide tout au long des étapes de connexion de [!DNL Google PubSub] (ci-après dénommé « [!DNL PubSub] ») à Experience Platform à l’aide de l’API [[!DNL Flow Service] ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à connecter [!DNL PubSub] à Platform à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL PubSub], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification basée sur un projet]

| Informations d’identification | Description |
| --- | --- |
| `projectId` | Identifiant de projet requis pour authentifier [!DNL PubSub]. |
| `credentials` | Informations d’identification requises pour l’authentification [!DNL PubSub]. Vous devez vous assurer de placer l’intégralité du fichier JSON après avoir supprimé les espaces blancs de vos informations d’identification. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions cible de base et source. L’identifiant de spécification de connexion [!DNL PubSub] est : `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Authentification par thème et par abonnement]

| Informations d’identification | Description |
| --- | --- |
| `credentials` | Informations d’identification requises pour l’authentification [!DNL PubSub]. Vous devez vous assurer de placer l’intégralité du fichier JSON après avoir supprimé les espaces blancs de vos informations d’identification. |
| `topicName` | Nom de la ressource qui représente un flux de messages. Vous devez spécifier un nom de rubrique si vous souhaitez donner accès à un flux de données spécifique dans votre [!DNL PubSub] source. Le format du nom de la rubrique est le suivant : `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Le nom de votre [!DNL PubSub] abonnement. Dans [!DNL PubSub], les abonnements permettent de recevoir des messages, en s’abonnant à la rubrique sur laquelle les messages ont été publiés. **Remarque**: une seule [!DNL PubSub] abonnement ne peut être utilisé que pour un seul flux de données. Pour créer plusieurs flux de données, vous devez disposer de plusieurs abonnements. Le format du nom de l&#39;abonnement est le suivant : `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions cible de base et source. L’identifiant de spécification de connexion [!DNL PubSub] est : `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Pour plus d’informations sur ces valeurs, voir le document d’[[!DNL PubSub] authentification](https://cloud.google.com/pubsub/docs/authentication). Pour utiliser l’authentification par compte de service, consultez le [[!DNL PubSub] Guide de création de comptes de service](https://cloud.google.com/docs/authentication/production#create_service_account) pour savoir comment générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créée, vous ne pouvez pas modifier le type d&#39;authentification d&#39;un [!DNL Google PubSub] connexion de base. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL PubSub] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL PubSub] dans le cadre des paramètres de requête.

La variable [!DNL PubSub] source vous permet de spécifier le type d’accès que vous souhaitez autoriser lors de l’authentification. Vous pouvez configurer votre compte pour qu’il dispose d’un accès racine ou restreindre l’accès à un [!DNL PubSub] rubrique et abonnement.

>[!NOTE]
>
>Entité de sécurité (rôles) affectée à une [!DNL PubSub] les projets sont hérités dans toutes les rubriques et tous les abonnements créés dans une [!DNL PubSub] projet. Si vous souhaitez qu’une entité (rôle) ait accès à une rubrique spécifique, cette entité (rôle) doit également être ajoutée à l’abonnement correspondant à la rubrique. Pour plus d’informations, consultez la section [[!DNL PubSub] documentation sur le contrôle d’accès](<https://cloud.google.com/pubsub/docs/access-control>).

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Authentification basée sur un projet]

Pour créer une connexion de base avec l’authentification basée sur le projet, envoyez une requête de POST à la fonction `/connections` endpoint et fournissez vos `projectId` et `credentials` dans le corps de la requête.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
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
| `auth.params.projectId` | Identifiant de projet requis pour authentifier [!DNL PubSub]. |
| `auth.params.credentials` | Informations d’identification ou clé requises pour authentifier [!DNL PubSub]. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL PubSub] : `70116022-a743-464a-bbfe-e226a7f8210c`. |

++++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant de connexion de base est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB Authentification par thème et par abonnement]

Pour créer une connexion de base avec l’authentification par sujet et par abonnement, envoyez une requête de POST à la fonction `/connections` endpoint et fournissez vos `credentials`, `topicName`, et `subscriptionName` dans le corps de la requête.

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
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
| `auth.params.credentials` | Informations d’identification ou clé requises pour authentifier [!DNL PubSub]. |
| `auth.params.topicName` | L’ID de projet et la paire d’ID de rubrique pour la [!DNL PubSub] source à laquelle vous souhaitez donner accès. |
| `auth.params.subscriptionName` | L’ID de projet et l’ID d’abonnement pour la [!DNL PubSub] source à laquelle vous souhaitez donner accès. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL PubSub] : `70116022-a743-464a-bbfe-e226a7f8210c`. |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant de connexion de base est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Créer une connexion source {#source}

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et un identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation.

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` de l’API [!DNL Flow Service].

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez fournir pour inclure plus d’informations sur votre connexion source. |
| `baseConnectionId` | Identifiant de connexion de base de votre source [!DNL PubSub] générée à l’étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion fixe pour [!DNL PubSub]. Cet ID est le suivant : `70116022-a743-464a-bbfe-e226a7f8210c`. |
| `data.format` | Format des données [!DNL PubSub] que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |
| `params.topicName` | Le nom de votre [!DNL PubSub] rubrique. Dans [!DNL PubSub], une rubrique est une ressource nommée qui représente un flux de messages. |
| `params.subscriptionName` | Nom de l’abonnement qui correspond à une rubrique donnée. Dans [!DNL PubSub], les abonnements permettent de lire les messages d’une rubrique. Un ou plusieurs abonnements peuvent être attribués à une seule rubrique. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Le tutoriel suivant requiert cet ID pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion source [!DNL PubSub] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet ID de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’API  [!DNL Flow Service] ](../../collect/streaming.md).
