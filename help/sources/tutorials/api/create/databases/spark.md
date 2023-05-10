---
keywords: Experience Platform;accueil;rubriques populaires;Apache Spark;spark apache;Azure HDInsights
solution: Experience Platform
title: Création d’une Apache Spark sur une connexion de base Azure HDInsights à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Apache Spark sur Azure HDInsights à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 61%

---

# Créez un [!DNL Apache Spark] on [!DNL Azure] Connexion de base HDInsights à l’aide de la variable [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Apache Spark] on [!DNL Azure HDInsights] Le connecteur est en version bêta. Voir la [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Apache Spark] on [!DNL Azure HDInsights] (ci-après dénommés &quot;[!DNL Spark]&quot;) en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Spark] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Spark], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | L’adresse IP ou le nom d’hôte de la variable [!DNL Spark] serveur. |
| `username` | Nom d’utilisateur auquel vous accédez [!DNL Spark] Serveur. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Spark] est : `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Pour plus d’informations sur la prise en main, reportez-vous à la section [ce document Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Spark] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Spark] :


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.host` | L’hôte de la variable [!DNL Spark] serveur. |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Spark] connexion. |
| `auth.params.password` | Le mot de passe associé à votre [!DNL Spark] connexion. |
| `connectionSpec.id` | Le [!DNL Spark] identifiant de spécification de connexion : `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Spark] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/database-nosql.md)
