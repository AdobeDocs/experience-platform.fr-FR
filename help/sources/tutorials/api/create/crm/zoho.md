---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Créez une connexion de base à Zoho CRM à l’aide de l’API Flow Service.
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Zoho CRM à l’aide de l’API Flow Service.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 96%

---

# Créez une connexion de base à [!DNL Zoho CRM] à l’aide de l’API [!DNL Flow Service].

>[!WARNING]
>
>La source [!DNL Zoho CRM] sera abandonnée fin juin 2025.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Zoho CRM] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour une connexion réussie à [!DNL Zoho CRM] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Zoho CRM], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `endpoint` | Point d’entrée du serveur [!DNL Zoho CRM] vers lequel vous effectuez votre demande. |
| `accountsUrl` | L’URL des comptes est utilisée pour générer vos jetons d’accès et d’actualisation. L’URL doit être spécifique au domaine. |
| `clientId` | Identifiant client correspondant à votre compte d’utilisateur [!DNL Zoho CRM]. |
| `clientSecret` | Secret client correspondant à votre compte d’utilisateur [!DNL Zoho CRM]. |
| `accessToken` | Le jeton d’accès autorise votre accès sécurisé et temporaire à votre compte [!DNL Zoho CRM]. |
| `refreshToken` | Un jeton d’actualisation est un jeton utilisé pour générer un nouveau jeton d’accès, une fois que votre jeton d’accès a expiré. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Zoho CRM] est `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Pour plus d’informations sur ces informations d’identification, consultez la documentation sur lʼ[[!DNL Zoho CRM] authentification](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Zoho CRM] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

>[!TIP]
>
>Votre domaine URL de comptes doit correspondre à l’emplacement de domaine approprié. Vous trouverez ci-dessous les différents domaines et leurs URL de comptes correspondantes :<ul><li>États-Unis : https://accounts.zoho.com</li><li>Australie : https://accounts.zoho.com.au</li><li>Europe : https://accounts.zoho.eu</li><li>Inde : https://accounts.zoho.in</li><li>Chine : https://accounts.zoho.com.cn</li></ul>

La requête suivante crée une connexion de base pour [!DNL Zoho CRM] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nom de votre connexion de base [!DNL Zoho CRM]. Vous pouvez utiliser ce nom pour rechercher votre connexion de base à [!DNL Zoho CRM]. |
| `description` | Description facultative de votre connexion de base à [!DNL Zoho CRM]. |
| `auth.specName` | Type d’authentification utilisé pour la connexion. |
| `auth.params.endpoint` | Point d’entrée du serveur [!DNL Zoho CRM] vers lequel vous effectuez une demande. |
| `auth.params.accountsUrl` | L’URL de comptes est utilisée pour générer vos jetons d’accès et d’actualisation. L’URL doit être spécifique au domaine. |
| `auth.params.clientId` | Identifiant client correspondant à votre compte d’utilisateur [!DNL Zoho CRM]. |
| `auth.params.clientSecret` | Secret client correspondant à votre compte d’utilisateur [!DNL Zoho CRM]. |
| `auth.params.accessToken` | Le jeton d’accès autorise votre accès sécurisé et temporaire à votre compte [!DNL Zoho CRM]. |
| `auth.params.refreshToken` | Un jeton d’actualisation est un jeton utilisé pour générer un nouveau jeton d’accès, une fois que votre jeton d’accès a expiré. |
| `connectionSpec.id` | Identifiant de spécification de connexion pour [!DNL Zoho CRM] : `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Zoho] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de gestion de la relation client dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/crm.md)
