---
keywords: Experience Platform;accueil;rubriques les plus consultées;Phoenix;phoenix
solution: Experience Platform
title: Création d’une connexion de base Phoenix à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter une base de données Phoenix à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 8%

---

# Créez une connexion de base [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le connecteur [!DNL Phoenix] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] sert à collecter et à centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise l’API [!DNL Flow Service] pour vous guider tout au long des étapes nécessaires pour connecter une base de données [!DNL Phoenix] à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Phoenix], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur [!DNL Phoenix]. |
| `username` | Nom d’utilisateur que vous utilisez pour accéder au serveur [!DNL Phoenix]. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `port` | Port TCP utilisé par le serveur [!DNL Phoenix] pour écouter les connexions client. Si vous vous connectez à [!DNL Azure] HDInsights, spécifiez le port 443. |
| `httpPath` | URL partielle correspondant au serveur [!DNL Phoenix]. Spécifiez /hbasephoenix0 si vous utilisez la grappe [!DNL Azure] HDInsights . |
| `enableSsl` | Une valeur booléenne. Indique si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Phoenix] est : `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Pour plus d’informations sur la prise en main, reportez-vous à [ce document Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Phoenix] dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Phoenix] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | L’hôte du serveur [!DNL Phoenix]. |
| `auth.params.username` | Nom d’utilisateur associé à votre connexion [!DNL Phoenix]. |
| `auth.params.password` | Mot de passe associé à votre connexion [!DNL Phoenix]. |
| `auth.params.port` | Port TCP de votre connexion [!DNL Phoenix]. |
| `auth.params.httpPath` | Chemin d’accès http partiel pour votre connexion [!DNL Phoenix]. |
| `auth.params.enableSsl` | Valeur boolean qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Phoenix] : `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer les bases de données à l’aide de l’API Flow Service](../../explore/database-nosql.md).
