---
title: Connecter des briques de données à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter des briques de données à Experience Platform à l’aide d’API.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 96e395e3b3d977d7eb04c400f6fd290977bf1101
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 17%

---

# Connexion de [!DNL Databricks] à Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!AVAILABILITY]
>
>* La source [!DNL Databricks] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>* La source [!DNL Databricks] est en version Beta. Lisez les [termes et conditions](../../../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Lisez ce guide pour savoir comment connecter votre compte [!DNL Databricks] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Lisez le guide sur [comment commencer à utiliser les API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

### Configuration de la configuration requise

Lisez la [[!DNL Databricks] présentation](../../../../connectors/databases/databricks.md) pour en savoir plus sur les configurations préalables qui doivent être effectuées avant de pouvoir connecter votre compte à Experience Platform.

### Collecter les informations d’identification requises

Fournissez des valeurs pour les informations d’identification suivantes afin de [!DNL Databricks] connecter à Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| `domain` | URL de votre espace de travail [!DNL Databricks]. Par exemple : `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | L’identifiant de votre cluster dans [!DNL Databricks]. Ce cluster doit déjà être un cluster existant et doit être un cluster interactif. |
| `accessToken` | Jeton d’accès qui authentifie votre compte [!DNL Databricks]. Vous pouvez générer votre jeton d’accès à l’aide de l’espace de travail [!DNL Databricks]. |
| `database` | Nom de votre base de données dans le lac delta. |
| `connectionSpec.Id` | L’identifiant de spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Databricks] est `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`. |

Pour plus d’informations, consultez la [[!DNL Databricks] vue d’ensemble](../../../../connectors/databases/databricks.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez les informations d’authentification appropriées pour votre compte [!DNL Databricks].

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour une source [!DNL Databricks] à l’aide de l’authentification par jeton d’accès.

+++Afficher l’exemple de requête

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Propriété | Description |
| --- | --- |
| `auth.params.domain` | URL de votre espace de travail [!DNL Databricks]. |
| `auth.params.clusterId` | L’identifiant de votre cluster dans [!DNL Databricks]. Ce cluster doit déjà être un cluster existant et doit être interactif |
| `auth.params.accessToken` | Jeton d’accès qui authentifie votre compte [!DNL Databricks]. |
| `auth.params.database` | Nom de votre base de données dans le lac delta. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Databricks]. |

+++

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris votre identifiant de connexion de base.

+++Afficher l’exemple de réponse

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion entre votre compte [!DNL Databricks] et Experience Platform. Vous pouvez utiliser l’identifiant de connexion de base que vous venez de générer dans les tutoriels suivants :

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
