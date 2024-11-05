---
title: Création d’une connexion de base Phoenix à l’aide de l’API Flow Service
description: Découvrez comment connecter une base de données Phoenix à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 37%

---

# Créez une connexion de base à [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service].

>[!IMPORTANT]
>
>La source [!DNL Phoenix] sera abandonnée fin mai 2025. Vous pouvez également utiliser la source [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel décrit les étapes à suivre pour créer une connexion de base et connecter votre compte [!DNL Phoenix] à Adobe Experience Platform à l’aide de l’API [!DNL Flow Service].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de services Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance d’Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Phoenix] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Vous devez fournir les informations d’authentification suivantes pour connecter votre compte [!DNL Phoenix] à Experience Platform.

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur [!DNL Phoenix]. |
| `username` | Nom d’utilisateur que vous utilisez pour accéder au serveur [!DNL Phoenix]. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `port` | Port TCP utilisé par le serveur [!DNL Phoenix] pour écouter les connexions client. Si vous vous connectez à [!DNL Azure HDInsights], spécifiez le port 443. Si ce paramètre n’est pas fourni, la valeur par défaut est 8765. |
| `httpPath` | URL partielle correspondant au serveur [!DNL Phoenix]. Spécifiez /hbasephoenix0 si vous utilisez la grappe [!DNL Azure] HDInsights . |
| `enableSsl` | Une valeur booléenne. Indique si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Phoenix] est : `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ce document Phoenix](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer une connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Phoenix] dans le corps de la requête.

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
| `auth.params.host` | L’hôte du serveur [!DNL Phoenix]. |
| `auth.params.username` | Nom d’utilisateur associé à votre connexion [!DNL Phoenix]. |
| `auth.params.password` | Mot de passe associé à votre connexion [!DNL Phoenix]. |
| `auth.params.port` | Le port TCP pour votre connexion [!DNL Phoenix]. |
| `auth.params.httpPath` | Chemin d’accès http partiel pour votre connexion [!DNL Phoenix]. |
| `auth.params.enableSsl` | Valeur boolean qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Phoenix] : `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

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
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
