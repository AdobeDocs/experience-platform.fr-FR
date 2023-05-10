---
keywords: Experience Platform;accueil;rubriques les plus consultées;Phoenix;phoenix
solution: Experience Platform
title: Création d’une connexion de base Phoenix à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter une base de données Phoenix à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 51%

---

# Créez une connexion de base à [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service].

>[!NOTE]
>
>Le [!DNL Phoenix] Le connecteur est en version bêta. Voir la [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

[!DNL Flow Service] sert à collecter et à centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Ce tutoriel utilise la méthode [!DNL Flow Service] API pour vous guider dans les étapes de connexion à un [!DNL Phoenix] vers la base de données [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Phoenix] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Phoenix], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | L’adresse IP ou le nom d’hôte de la variable [!DNL Phoenix] serveur. |
| `username` | Nom d’utilisateur auquel vous accédez [!DNL Phoenix] Serveur. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `port` | Le port TCP que la variable [!DNL Phoenix] Le serveur utilise pour écouter les connexions client. Si vous vous connectez à [!DNL Azure] HDInsights, spécifiez le port 443. |
| `httpPath` | L’URL partielle correspondant au [!DNL Phoenix] serveur. Spécifiez /hbasephoenix0 si vous utilisez [!DNL Azure] Grappe HDInsights . |
| `enableSsl` | Une valeur booléenne. Indique si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Phoenix] est : `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Pour plus d’informations sur la prise en main, reportez-vous à la section [ce document Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Phoenix] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Phoenix] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}",
            "port": {PORT},
            "httpPath": "{PATH}",
            "enableSsl": {SSL}
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
| `auth.params.host` | L’hôte de la variable [!DNL Phoenix] serveur. |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Phoenix] connexion. |
| `auth.params.password` | Le mot de passe associé à votre [!DNL Phoenix] connexion. |
| `auth.params.port` | Le port TCP pour votre [!DNL Phoenix] connexion. |
| `auth.params.httpPath` | Le chemin d’accès http partiel pour votre [!DNL Phoenix] connexion. |
| `auth.params.enableSsl` | Valeur boolean qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | Le [!DNL Phoenix] identifiant de spécification de connexion : `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/database-nosql.md)
