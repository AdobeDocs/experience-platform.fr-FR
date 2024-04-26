---
title: Création d’une connexion de base PathFactory à l’aide de l’API Flow Service
description: Découvrez comment authentifier votre compte PathFactory par rapport à Experience Platform à l’aide de l’API Flow Service.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Version Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 46%

---

# Créez une connexion de base à [!DNL PathFactory] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Lisez ce document pour savoir comment créer une connexion de base pour [!DNL PathFactory] en utilisant la variable [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL PathFactory] en utilisant la variable [!DNL Flow Service] API.

### Collecte des informations d’identification requises {#gather-credentials}

Pour accéder à votre compte PathFactory sur Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Nom d’utilisateur | Votre [!DNL PathFactory] nom d’utilisateur du compte. Ceci est essentiel pour identifier votre compte dans le système. |
| Mot de passe | Le mot de passe associé à votre [!DNL PathFactory] compte . Veillez à ce que cette protection soit sécurisée pour empêcher tout accès non autorisé. |
| Domaine | Le domaine associé à votre [!DNL PathFactory] compte . Cela fait généralement référence à l’identifiant unique de votre [!DNL PathFactory] URL. |
| Jeton d’accès | Jeton unique utilisé pour l’authentification API pour assurer une communication sécurisée entre vos systèmes et [!DNL PathFactory]. |
| Points de terminaison API | Points de terminaison d’API spécifiques pour l’accès aux données : visiteurs, sessions et pages vues. Chaque point de terminaison correspond à différents jeux de données que vous pouvez récupérer. **Remarque :** Ils sont prédéfinis par [!DNL PathFactory] et sont spécifiques aux données auxquelles vous avez l’intention d’accéder : <ul><li>**Point de terminaison Visiteurs**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Point de terminaison des sessions**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Point de terminaison des pages vues**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Pour plus d’informations sur la manière de sécuriser et d’utiliser vos informations d’identification, ainsi que sur la manière d’obtenir et d’actualiser votre jeton d’accès, consultez la page [[!DNL PathFactory] Centre d’assistance](https://support.pathfactory.com/categories/adobe/). Cette ressource propose des guides complets sur la gestion de vos informations d’identification et sur l’intégration efficace et sécurisée de l’API.

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL PathFactory] informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL PathFactory] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.clientId` | L’ID client associé à votre [!DNL PathFactory] application. |
| `auth.params.clientSecret` | Le secret client associé à votre [!DNL PathFactory] application. |
| `connectionSpec.id` | La variable [!DNL PathFactory] identifiant de spécification de connexion : `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL PathFactory] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer les données d’automatisation du marketing dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
