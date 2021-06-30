---
keywords: Experience Platform;accueil;rubriques les plus consultées;Apache Hadoop Distributed File System;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Création d’une connexion de base Apache HDFS à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter un Apache Hadoop Distributed File System à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 12%

---

# Créez une connexion de base [!DNL Apache] HDFS à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le connecteur Apache HDFS est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Apache Hadoop Distributed File System] (ci-après appelée &quot;[!DNL HDFS]&quot;) à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL HDFS] à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

| Credential | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour se connecter à [!DNL HDFS] de manière anonyme. Pour plus d’informations sur la manière d’obtenir cette valeur, voir [this [!DNL HDFS] document](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL AdWords] est : `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL HDFS] dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL HDFS] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.url` | L’URL qui définit les paramètres d’authentification requis pour se connecter à [!DNL HDFS] de manière anonyme |
| `connectionSpec.id` | ID de spécification de connexion [!DNL HDFS] : `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL HDFS] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer un espace de stockage cloud tiers à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
