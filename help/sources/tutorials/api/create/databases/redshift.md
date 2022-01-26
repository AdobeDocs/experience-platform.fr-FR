---
keywords: Experience Platform;accueil;rubriques les plus consultées;redshift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Création d’une connexion de base de Redshift Amazon à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Amazon Redshift à l’aide de l’API Flow Service.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 2fb972b0ec8d1f679c6ce104a439265b5cc4d535
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 11%

---

# Créez un [!DNL Amazon Redshift] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Amazon Redshift] en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Amazon Redshift] en utilisant la variable [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Amazon Redshift], vous devez fournir les propriétés de connexion suivantes :

| **Credential** | **Description** |
| -------------- | --------------- |
| `server` | Le serveur associé à votre [!DNL Amazon Redshift] compte . |
| `username` | Le nom d’utilisateur associé à votre [!DNL Amazon Redshift] compte . |
| `password` | Le mot de passe associé à votre [!DNL Amazon Redshift] compte . |
| `database` | Le [!DNL Amazon Redshift] base de données à laquelle vous accédez. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Amazon Redshift] is `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Amazon Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

>[!NOTE]
>
>La norme de codage par défaut pour [!DNL Redshift] est Unicode. Cela ne peut pas être modifié.

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Amazon Redshift] informations d’identification d’authentification dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| ------------- | --------------- |
| `auth.params.server` | Votre [!DNL Amazon Redshift] serveur. |
| `auth.params.database` | La base de données associée à votre [!DNL Amazon Redshift] compte . |
| `auth.params.password` | Le mot de passe associé à votre [!DNL Amazon Redshift] compte . |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Amazon Redshift] compte . |
| `connectionSpec.id` | Le [!DNL Amazon Redshift] identifiant de spécification de connexion : `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Amazon Redshift] connexion à l’aide de la fonction [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion dans le tutoriel suivant pendant que vous apprenez à [explorer des bases de données ou des systèmes NoSQL à l’aide de l’API Flow Service](../../explore/database-nosql.md).
