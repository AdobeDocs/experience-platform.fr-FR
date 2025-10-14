---
title: Créer une connexion source Google PubSub à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un compte Google PubSub à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 45%

---

# Créer une connexion source [!DNL Google PubSub] à l’aide de l’API Flow Service

>[!IMPORTANT]
>
>La source [!DNL Google PubSub] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Ce tutoriel vous guide tout au long des étapes de connexion de [!DNL Google PubSub] (ci-après dénommé « [!DNL PubSub] ») à Experience Platform à l’aide de l’API [[!DNL Flow Service] &#x200B;](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à connecter [!DNL PubSub] à Experience Platform à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les propriétés de connexion décrites ci-dessous afin de connecter votre compte [!DNL PubSub] à [!DNL Flow Service]. Pour plus d’informations sur l’authentification et la configuration requise, consultez la [[!DNL PubSub source] présentation](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB Authentification basée sur le projet]

| Informations d’identification | Description |
| --- | --- |
| `projectId` | Identifiant de projet requis pour authentifier [!DNL PubSub]. |
| `credentials` | Informations d’identification requises pour authentifier [!DNL PubSub]. Vous devez vous assurer de placer le fichier JSON complet après avoir supprimé les espaces blancs de vos informations d’identification. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et cible source. L’identifiant de spécification de connexion [!DNL PubSub] est : `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB Authentification par rubrique et par abonnement]

| Informations d’identification | Description |
| --- | --- |
| `credentials` | Informations d’identification requises pour authentifier [!DNL PubSub]. Vous devez vous assurer de placer le fichier JSON complet après avoir supprimé les espaces blancs de vos informations d’identification. |
| `topicName` | Nom de la ressource qui représente un flux de messages. Vous devez spécifier un nom de rubrique si vous souhaitez donner accès à un flux de données spécifique dans votre source de [!DNL PubSub]. Le format du nom du topic est : `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | Nom de votre abonnement [!DNL PubSub]. Dans [!DNL PubSub], les abonnements vous permettent de recevoir des messages, en vous abonnant à la rubrique dans laquelle les messages ont été publiés. **Remarque** : un seul abonnement [!DNL PubSub] ne peut être utilisé que pour un seul flux de données. Pour créer plusieurs flux de données, vous devez disposer de plusieurs abonnements. Le format du nom de l’abonnement est : `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et cible source. L’identifiant de spécification de connexion [!DNL PubSub] est : `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

Pour plus d’informations sur ces valeurs, consultez ce document [[!DNL PubSub] authentification](https://cloud.google.com/pubsub/docs/authentication). Pour utiliser l’authentification par compte de service, lisez ce [[!DNL PubSub] guide sur la création de comptes de service](https://cloud.google.com/docs/authentication/production#create_service_account) pour savoir comment générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Google PubSub]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

La première étape de création d’une connexion source consiste à authentifier votre source [!DNL PubSub] et à générer un identifiant de connexion de base. Un identifiant de connexion de base vous permet d’explorer et de parcourir les fichiers de votre source et d’identifier les éléments spécifiques à ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL PubSub] dans le cadre des paramètres de requête.

La source [!DNL PubSub] vous permet de spécifier le type d’accès que vous souhaitez autoriser lors de l’authentification. Vous pouvez configurer votre compte pour disposer d’un accès racine ou restreindre l’accès à une rubrique de [!DNL PubSub] et à un abonnement spécifiques.

>[!NOTE]
>
>Les principaux (rôles) affectés à un projet [!DNL PubSub] sont hérités dans toutes les rubriques et tous les abonnements créés dans un projet [!DNL PubSub]. Si vous souhaitez qu’un principal (rôle) ait accès à une rubrique spécifique, ce principal (rôle) doit également être ajouté à l’abonnement correspondant à la rubrique. Pour plus d’informations, consultez la [[!DNL PubSub] documentation sur le contrôle d’accès](<https://cloud.google.com/pubsub/docs/access-control>).

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Authentification basée sur le projet]

Pour créer une connexion de base avec l’authentification par projet, envoyez une requête POST au point d’entrée `/connections` et indiquez vos `projectId` et `credentials` dans le corps de la requête.

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

>[!TAB Authentification par rubrique et par abonnement]

Pour créer une connexion de base avec l’authentification par rubrique et par abonnement, envoyez une requête POST au point d’entrée `/connections` et indiquez vos `credentials`, `topicName` et `subscriptionName` dans le corps de la requête.

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
| `auth.params.topicName` | Paire d’ID de projet et d’ID de rubrique pour la source de [!DNL PubSub] à laquelle vous souhaitez accorder l’accès. |
| `auth.params.subscriptionName` | Paire d’ID de projet et d’ID d’abonnement pour la source de [!DNL PubSub] à laquelle vous souhaitez fournir un accès. |
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
| `params.topicName` | Nom de la rubrique [!DNL PubSub]. Dans [!DNL PubSub], une rubrique est une ressource nommée qui représente un flux de messages. |
| `params.subscriptionName` | Nom de l’abonnement qui correspond à une rubrique donnée. Dans [!DNL PubSub], les abonnements vous permettent de lire des messages à partir d’une rubrique. Un ou plusieurs abonnements peuvent être affectés à une seule rubrique. |
| `params.dataType` | Ce paramètre définit le type des données ingérées. Les types de données pris en charge sont les suivants : `raw` et `xdm`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Le tutoriel suivant requiert cet ID pour créer un flux de données.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Après avoir créé ou mis à jour un flux de données en continu, une brève pause de 5 minutes dans l’ingestion des données est nécessaire pour éviter toute instance potentielle de perte de données ou d’abandon de données.

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion source [!DNL PubSub] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet ID de connexion source dans le tutoriel suivant pour [créer un flux de données en continu à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/streaming.md).
