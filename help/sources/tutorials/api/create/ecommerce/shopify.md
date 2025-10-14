---
keywords: Experience Platform;accueil;rubriques populaires;Shopify;shopify;e-commerce
solution: Experience Platform
title: Créer une connexion de base au connecteur Shopify à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Shopify à Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 49%

---

# Créez une connexion de base à [!DNL Shopify] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion de base pour [!DNL Shopify] (ci-après dénommée « [!DNL Shopify] ») à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Sources]](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Shopify] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Shopify], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Point d’entrée de votre serveur [!DNL Shopify]. |
| `accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Shopify] est `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

Pour plus d’informations sur la prise en main, consultez ce [document d’authentification Shopify](https://shopify.dev/concepts/about-apis/authentication).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Shopify] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Shopify] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | Point d’entrée du serveur [!DNL Shopify]. |
| `auth.params.accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Shopify] : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Shopify] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer des données E-Commerce dans Experience Platform à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/ecommerce.md)
