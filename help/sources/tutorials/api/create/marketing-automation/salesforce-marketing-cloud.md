---
keywords: Experience Platform;accueil;rubriques les plus consultées;Salesforce marketing cloud;Marketing Cloud Salesforce
solution: Experience Platform
title: Création d’une connexion de base de Marketing Cloud Salesforce à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform au Marketing Cloud Salesforce à l’aide de l’API Flow Service.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 61%

---

# Créez une connexion de base à [!DNL Salesforce Marketing Cloud] à l’aide de l’API [!DNL Flow Service].

>[!NOTE]
>
>La source [!DNL Salesforce Marketing Cloud] est en version Beta. Voir la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta. 

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Salesforce Marketing Cloud] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md)[!DNL Platform] : Experience  permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md)[!DNL Platform] : Experience  fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Salesforce Marketing Cloud] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Salesforce Marketing Cloud], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Serveur hôte de votre application. Il s’agit souvent de votre sous-domaine. **Remarque :** Lorsque vous saisissez votre `host` , il vous suffit de spécifier le sous-domaine et non l’URL entière. Par exemple, si l’URL d’hôte est `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, il vous suffit de saisir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` comme valeur d’hôte. |
| `clientId` | L’ID client associé à votre [!DNL Salesforce Marketing Cloud] application. |
| `clientSecret` | Le secret client associé à votre [!DNL Salesforce Marketing Cloud] application. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Salesforce Marketing Cloud] est `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Salesforce Marketing Cloud] informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Salesforce Marketing Cloud] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
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
| `auth.params.clientId` | L’ID client associé à votre [!DNL Salesforce Marketing Cloud] application. |
| `auth.params.clientSecret` | Le secret client associé à votre [!DNL Salesforce Marketing Cloud] application. |
| `connectionSpec.id` | Le [!DNL Salesforce Marketing Cloud] identifiant de spécification de connexion : `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de , y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Salesforce Marketing Cloud] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer les données d’automatisation du marketing dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
