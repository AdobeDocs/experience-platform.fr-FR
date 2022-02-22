---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Création d’une connexion de base CRM Zoho à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Zoho CRM à l’aide de l’API Flow Service.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 8%

---

# Créez un [!DNL Zoho CRM] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Zoho CRM] en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d&#39;Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour vous connecter à [!DNL Zoho CRM] en utilisant la variable [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Zoho CRM], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| --- | --- |
| `endpoint` | Le point de terminaison de [!DNL Zoho CRM] le serveur vers lequel vous effectuez votre demande. |
| `accountsUrl` | L’URL des comptes est utilisée pour générer vos jetons d’accès et d’actualisation. L’URL doit être spécifique au domaine. |
| `clientId` | L’identifiant client qui correspond à votre [!DNL Zoho CRM] compte utilisateur. |
| `clientSecret` | Le secret client qui correspond à votre [!DNL Zoho CRM] compte utilisateur. |
| `accessToken` | Le jeton d’accès autorise votre accès sécurisé et temporaire à votre [!DNL Zoho CRM] compte . |
| `refreshToken` | Un jeton d’actualisation est un jeton utilisé pour générer un nouveau jeton d’accès, une fois que votre jeton d’accès a expiré. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Zoho CRM] est : `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Pour plus d’informations sur ces informations d’identification, consultez la documentation sur [[!DNL Zoho CRM] authentication](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Zoho CRM] informations d’identification d’authentification dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

>[!TIP]
>
>Votre domaine URL de compte doit correspondre à l’emplacement de domaine approprié. Vous trouverez ci-dessous les différents domaines et les URL de leurs comptes correspondants :<ul><li>États-Unis : https://accounts.zoho.com</li><li>Australie : https://accounts.zoho.com.au</li><li>Europe : https://accounts.zoho.eu</li><li>Inde : https://accounts.zoho.in</li><li>Chine : https://accounts.zoho.com.cn</li></ul>

La requête suivante crée une connexion de base pour [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Le nom de votre [!DNL Zoho CRM] connexion de base. Vous pouvez utiliser ce nom pour rechercher votre [!DNL Zoho CRM] connexion de base. |
| `description` | Une description facultative de votre [!DNL Zoho CRM] connexion de base. |
| `auth.specName` | Type d’authentification utilisé pour la connexion. |
| `auth.params.endpoint` | Le point de terminaison de [!DNL Zoho CRM] le serveur vers lequel vous effectuez votre demande. |
| `auth.params.accountsUrl` | L’URL des comptes est utilisée pour générer vos jetons d’accès et d’actualisation. L’URL doit être spécifique au domaine. |
| `auth.params.clientId` | L’identifiant client qui correspond à votre [!DNL Zoho CRM] compte utilisateur. |
| `auth.params.clientSecret` | Le secret client qui correspond à votre [!DNL Zoho CRM] compte utilisateur. |
| `auth.params.accessToken` | Le jeton d’accès autorise votre accès sécurisé et temporaire à votre [!DNL Zoho CRM] compte . |
| `auth.params.refreshToken` | Un jeton d’actualisation est un jeton utilisé pour générer un nouveau jeton d’accès, une fois que votre jeton d’accès a expiré. |
| `connectionSpec.id` | L’identifiant de spécification de connexion pour [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Zoho CRM] connexion de base à l’aide de [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [exploration des systèmes CRM à l’aide de l’API Flow Service ;](../../explore/crm.md).
