---
keywords: Experience Platform;accueil;rubriques les plus consultées;Oracle Service Cloud;oracle service cloud
title: Création d’une connexion source cloud Oracle Service à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Oracle Service Cloud à l’aide de l’API Flow Service.
source-git-commit: 078a266967cd7b0818f958283a58a8af4c886a21
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 33%

---

# (Version bêta) Créez une connexion source Oracle Service Cloud à l’aide du [!DNL Flow Service] API

>[!NOTE]
>
>La source Oracle Service Cloud est en version bêta. Voir [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion de base pour Oracle Service Cloud à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à Oracle Service Cloud à l’aide du [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à Oracle Service Cloud, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | URL d’hôte de votre instance Oracle Service Cloud. |
| `username` | Nom d’utilisateur de votre compte utilisateur Oracle Service Cloud. |
| `password` | Mot de passe de votre compte Oracle Service Cloud. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour Oracle Service Cloud est : `ba5126ec-c9ac-11eb-b8bc-0242ac130003`. |

Pour plus d’informations sur l’authentification de votre compte Oracle Service Cloud, reportez-vous à la section [[!DNL Oracle] guide sur l&#39;authentification](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison tout en fournissant vos informations d’authentification Oracle Service Cloud dans le cadre des paramètres de requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour Oracle Service Cloud :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.host` | URL d’hôte de votre instance Oracle Service Cloud. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte Oracle Service Cloud. |
| `auth.params.password` | mot de passe associé à votre compte Oracle Service Cloud. |
| `connectionSpec.id` | L’identifiant de spécification de connexion Oracle Service Cloud : `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre système CRM à l’étape suivante.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion à la base Oracle Service Cloud à l’aide de la variable [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants :

* [Explorez la structure et le contenu de vos tableaux de données à l’aide du [!DNL Flow Service] API](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de succès client dans Platform à l’aide de la variable [!DNL Flow Service] API](../../collect/customer-success.md)
