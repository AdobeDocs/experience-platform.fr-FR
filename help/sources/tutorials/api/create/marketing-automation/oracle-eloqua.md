---
title: Créer une connexion de base Oracle Eloqua à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Oracle Eloqua à l’aide de l’API Flow Service.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 59%

---

# Créer une connexion de base [!DNL Oracle Eloqua] à l’aide de l’API [!DNL Flow Service]

>[!WARNING]
>
>La source [!DNL Oracle Eloqua] sera abandonnée à la fin du mois de juin 2025.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Oracle Eloqua] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour une connexion réussie à [!DNL Oracle Eloqua] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Oracle Eloqua], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `endpoint` | Point d’entrée de votre [!DNL Oracle Eloqua]. |
| `username` | Nom d’utilisateur de votre compte [!DNL Oracle Eloqua]. Le nom d’utilisateur doit être au format `siteName + \\ + username`, où `siteName` correspond au nom de la société avec laquelle vous vous êtes connecté à [!DNL Oracle Eloqua] et `username` correspond à votre nom d’utilisateur. Par exemple, votre nom d&#39;utilisateur de connexion peut être : `adobe\\emily`. |
| `password` | Mot de passe correspondant à votre nom d’utilisateur [!DNL Oracle Eloqua]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. La valeur de l’identifiant de spécification de connexion de la source [!DNL Oracle Eloqua] est fixe comme suit : `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Pour plus d’informations sur les informations d’authentification pour [!DNL Oracle Eloqua], reportez-vous au guide [[!DNL Oracle Eloqua] sur l’authentification](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Oracle Eloqua] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Oracle Eloqua] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Nom de votre connexion de base [!DNL Oracle Eloqua]. Il est recommandé de fournir un nom explicite, car vous pouvez utiliser cette valeur pour rechercher votre connexion de base. |
| `description` | (Facultatif) Propriété que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `auth.specName` | Type d’authentification utilisé pour la connexion. |
| `auth.params.endpoint` | Point d’entrée de votre serveur [!DNL Oracle Eloqua]. |
| `auth.params.username` | Informations d’identification concaténées incluant le nom du site et le nom d’utilisateur correspondant à votre compte [!DNL Oracle Eloqua]. |
| `auth.params.password` | Mot de passe correspondant à votre compte [!DNL Oracle Eloqua]. |
| `connectionSpec.id` | La valeur de l’identifiant de spécification de connexion de la source [!DNL Oracle Eloqua] est fixe comme suit : `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base [!DNL Oracle Eloqua] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer des données d’automatisation marketing dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
