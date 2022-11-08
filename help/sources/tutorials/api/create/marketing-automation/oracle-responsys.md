---
keywords: Experience Platform;accueil;rubriques les plus consultées;oracle;
title: (Version bêta) Création d’une connexion de base Responsys Oracle à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Oracle Responsys à l’aide de l’API Flow Service.
source-git-commit: aa4573325f2859c258e66d4b6df411118a5d1942
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 57%

---

# (Version bêta) Créez une [!DNL Oracle Responsys] connexion de base à l’aide de [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Oracle Responsys] La source est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs bêta-étiquetés.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Oracle Responsys] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants de Platform :

* [Sources](../../../../home.md) : Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md)[!DNL Platform] :  fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour une connexion réussie à [!DNL Oracle Responsys] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Oracle Responsys], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `endpoint` | L’URL du point d’entrée de l’authentification REST de votre [!DNL Oracle Responsys] instance. |
| `clientId` | Identifiant client de l’instance [!DNL Oracle Responsys]. |
| `clientSecret` | Secret client de l’instance [!DNL Oracle Responsys]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. La valeur de l’identifiant de spécification de connexion de la variable [!DNL Oracle Responsys] source est fixe comme suit : `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Pour plus d’informations sur les informations d’authentification pour [!DNL Oracle Responsys], reportez-vous à la section [[!DNL Oracle Responsys] guide sur l&#39;authentification](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Oracle Responsys] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Oracle Responsys] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Nom de votre connexion de base [!DNL Oracle Responsys]. Il est recommandé de fournir un nom explicite, car vous pouvez utiliser cette valeur pour rechercher votre connexion de base. |
| `description` | (Facultatif) Une propriété que vous pouvez inclure pour fournir des informations supplémentaires sur votre connexion de base. |
| `auth.specName` | Type d’authentification utilisé pour la connexion. |
| `auth.params.endpoint` | L’URL du point d’entrée de l’authentification REST de votre [!DNL Oracle Responsys] serveur. |
| `auth.params.clientId` | Identifiant client de l’instance [!DNL Oracle Responsys]. |
| `auth.params.clientSecret` | Secret client de l’instance [!DNL Oracle Responsys]. |
| `connectionSpec.id` | La valeur de l’identifiant de spécification de connexion de la variable [!DNL Oracle Responsys] source est fixe comme suit : `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Oracle Responsys] connexion de base à l’aide de [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants :

* [Explorez la structure et le contenu de vos tableaux de données à l’aide du [!DNL Flow Service] API](../../explore/tabular.md)
* [Créez un flux de données pour importer des données d’automatisation marketing dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/marketing-automation.md)
