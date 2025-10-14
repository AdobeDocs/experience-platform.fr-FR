---
title: Connecter AWS Redshift à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à AWS Redshift à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 30%

---

# Connexion de [!DNL AWS Redshift] à Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>La source [!DNL AWS Redshift] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce guide pour savoir comment connecter votre compte source [!DNL AWS Redshift] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Connecter [!DNL AWS Redshift] à Experience Platform sur Azure {#azure}

Pour plus d’informations sur la connexion de votre source [!DNL AWS Redshift] à Experience Platform sur Azure, lisez les étapes ci-dessous.

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puissiez vous connecter à [!DNL AWS Redshift], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| `server` | Nom du serveur de votre instance [!DNL AWS Redshift]. |
| `port` | Port TCP utilisé par un serveur [!DNL AWS Redshift] pour écouter les connexions client. |
| `username` | Nom d’utilisateur associé à votre compte [!DNL AWS Redshift]. |
| `password` | Mot de passe correspondant au compte utilisateur. |
| `database` | Base de données [!DNL AWS Redshift] à partir de laquelle les données doivent être récupérées. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL AWS Redshift] est `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Pour plus d’informations sur la prise en main, reportez-vous à ce [[!DNL AWS Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Créer une connexion de base pour [!DNL AWS Redshift] sur Experience Platform sur Azure [#azure-base]

>[!NOTE]
>
>La norme de codage par défaut pour [!DNL Redshift] est Unicode. Ceci ne peut pas être modifié.

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL AWS Redshift] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

+++Sélectionner pour afficher l’exemple

La requête suivante permet de créer une connexion de base pour [!DNL AWS Redshift] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | Nom du serveur de votre instance [!DNL AWS Redshift]. |
| `auth.params.port` | Port TCP utilisé par un serveur [!DNL AWS Redshift] pour écouter les connexions client. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL AWS Redshift]. |
| `auth.params.password` | Mot de passe correspondant au compte utilisateur. |
| `auth.params.database` | Base de données [!DNL AWS Redshift] à partir de laquelle les données doivent être récupérées. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL AWS Redshift] : `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

+++

**Réponse**

+++Sélectionner pour afficher l’exemple

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## Connexion de [!DNL AWS Redshift] à Experience Platform sur AWS Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur AWS Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre source [!DNL AWS Redshift] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL AWS Redshift] sur Experience Platform sur AWS {#aws-base}

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL AWS Redshift] :

+++Sélectionner pour afficher l’exemple

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | Nom du serveur de votre instance [!DNL AWS Redshift]. |
| `auth.params.port` | Port TCP utilisé par un serveur [!DNL AWS Redshift] pour écouter les connexions client. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL AWS Redshift]. |
| `auth.params.password` | Mot de passe correspondant au compte utilisateur. |
| `auth.params.database` | Base de données [!DNL AWS Redshift] à partir de laquelle les données doivent être récupérées. |
| `auth.params.schema` | Nom du schéma associé à votre base de données [!DNL AWS Redshift]. Vous devez vous assurer que l’utilisateur auquel vous souhaitez accorder l’accès à la base de données a également accès à ce schéma. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL AWS Redshift] : `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre stockage dans le tutoriel suivant.

+++Sélectionner pour afficher l’exemple

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base [!DNL AWS Redshift] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
