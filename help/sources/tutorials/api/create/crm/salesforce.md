---
keywords: Experience Platform;accueil;rubriques les plus consultées;Salesforce;Salesforce
solution: Experience Platform
title: Création d’une connexion de base Salesforce à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un compte Salesforce à l’aide de l’API Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 62%

---

# Créez une connexion de base à [!DNL Salesforce] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Salesforce] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Platform] à [!DNL Salesforce] à l’aide du [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Salesforce], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `environmentUrl` | L’URL de la variable [!DNL Salesforce] instance source. |
| `username` | Nom d’utilisateur de la variable [!DNL Salesforce] compte utilisateur. |
| `password` | Le mot de passe du [!DNL Salesforce] compte utilisateur. |
| `securityToken` | Jeton de sécurité pour la variable [!DNL Salesforce] compte utilisateur. |
| `apiVersion` | (Facultatif) La version de l’API REST de la variable [!DNL Salesforce] que vous utilisez. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce] est `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Pour plus d’informations sur la prise en main, voir [ce document Salesforce ;](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` endpoint et fournissez vos [!DNL Salesforce] informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Salesforce] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Connection",
      "description": "Connection for Salesforce account",
      "auth": {
          "specName": "Basic Authentication",
          "params": {****
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Salesforce] compte . |
| `auth.params.password` | Le mot de passe associé à votre [!DNL Salesforce] compte . |
| `auth.params.securityToken` | Le jeton de sécurité associé à votre [!DNL Salesforce] compte . |
| `connectionSpec.id` | La variable [!DNL Salesforce] identifiant de spécification de connexion : `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante. 

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Salesforce] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de gestion de la relation client dans Platform à l’aide du [!DNL Flow Service] API](../../collect/crm.md)
