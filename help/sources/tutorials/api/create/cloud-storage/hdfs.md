---
keywords: Experience Platform;accueil;rubriques populaires;Système de fichiers distribué Apache Hadoop;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Créer une connexion de base Apache HDFS à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter un système de fichiers distribué Apache Hadoop à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 43%

---

# Créer une connexion de base HDFS [!DNL Apache] à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le connecteur Apache HDFS est en version bêta. Consultez la [&#x200B; Présentation des sources &#x200B;](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion de base pour [!DNL Apache Hadoop Distributed File System] (ci-après dénommée « [!DNL HDFS] ») à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL HDFS] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour se connecter à [!DNL HDFS] de manière anonyme. Pour plus d’informations sur la façon d’obtenir cette valeur, reportez-vous à [ce [!DNL HDFS] document](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL AdWords] est `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL HDFS] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL HDFS] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.url` | URL qui définit les paramètres d’authentification requis pour se connecter à [!DNL HDFS] de manière anonyme |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL HDFS] : `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion [!DNL HDFS] à l’aide de l’API [!DNL Flow Service] et d’obtenir la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer un stockage cloud tiers à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
