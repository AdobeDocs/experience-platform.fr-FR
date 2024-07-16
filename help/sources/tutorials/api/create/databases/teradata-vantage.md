---
keywords: Experience Platform;accueil;rubriques les plus consultées;Teradata Vantage
title: Création d’une connexion de base de Teradata Vantage à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Teradata Vantage à l’aide de l’API Flow Service.
exl-id: 88707dca-3c7a-43c7-9d71-473ad9715fc6
source-git-commit: 625a7959f48a0b16c3228d4555e046b5f67c51b7
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 57%

---

# Créez une connexion de base à [!DNL Teradata Vantage] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Teradata Vantage] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Teradata Vantage] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Teradata Vantage], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `connectionString` | Une chaîne de connexion est une chaîne qui fournit des informations sur une source de données et sur la manière dont vous pouvez vous y connecter. Le modèle de chaîne de connexion pour [!DNL Teradata Vantage] est `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Teradata Vantage] est : `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

Pour plus d&#39;informations sur la prise en main, consultez ce [[!DNL Teradata Vantage] document](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Teradata Vantage] dans le cadre du corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Teradata Vantage] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à votre instance [!DNL Teradata Vantage]. Le modèle de chaîne de connexion pour [!DNL Teradata Vantage] est `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Teradata Vantage] : `2fa8af9c-2d1a-43ea-a253-f00a00c74412`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Teradata Vantage] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
