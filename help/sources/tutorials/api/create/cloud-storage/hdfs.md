---
keywords: Experience Platform;accueil;rubriques les plus consultées;Apache Hadoop Distributed File System;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Création d’une connexion de base Apache HDFS à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter un Apache Hadoop Distributed File System à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 61%

---

# Créez un [!DNL Apache] Connexion de base HDFS à l’aide de [!DNL Flow Service] API

>[!NOTE]
>
>Le connecteur Apache HDFS est en version bêta. Voir la [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Apache Hadoop Distributed File System] (ci-après dénommés &quot;[!DNL HDFS]&quot;) en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL HDFS] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour la connexion à [!DNL HDFS] anonymement. Pour plus d&#39;informations sur l&#39;obtention de cette valeur, reportez-vous à la section [this [!DNL HDFS] document](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL AdWords] est `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

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
| `auth.params.url` | L’URL qui définit les paramètres d’authentification requis pour la connexion à [!DNL HDFS] anonymement |
| `connectionSpec.id` | Le [!DNL HDFS] identifiant de spécification de connexion : `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Étapes suivantes

Vous êtes arrivé au bout de ce tutoriel, félicitations ! Grâce à celui-ci, vous avez créé une connexion de à [!DNL HDFS] à l’aide de l’API [!DNL Flow Service] et avez obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer un espace de stockage dans le cloud tiers à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
