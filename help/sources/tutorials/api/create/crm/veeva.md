---
keywords: Experience Platform;accueil;rubriques populaires;veeva crm;Veeva CRM;Veeva CRM;
solution: Experience Platform
title: Créer une connexion de base Veeva CRM à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Veeva CRM à l’aide de l’API Flow Service.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 68%

---

# Créez une connexion de base à [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Veeva CRM] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour une connexion réussie à [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Veeva CRM], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `environmentUrl` | URL de votre instance [!DNL Veeva CRM]. |
| `username` | Valeur du nom d’utilisateur de votre compte [!DNL Veeva CRM]. |
| `password` | Valeur du mot de passe de votre compte [!DNL Veeva CRM]. |
| `securityToken` | Jeton de sécurité de votre instance [!DNL Veeva CRM]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Veeva CRM] est `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Pour plus d’informations sur ces valeurs, reportez-vous à ce [[!DNL Veeva CRM] document](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Veeva CRM] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Veeva CRM] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Nom de votre connexion de base [!DNL Veeva CRM]. Vous pouvez utiliser ce nom pour rechercher votre connexion de base à [!DNL Veeva CRM]. |
| `description` | Description facultative de votre connexion de base à [!DNL Veeva CRM]. |
| `auth.specName` | Type d’authentification utilisé pour la connexion. |
| `auth.params.environmentUrl` | URL de votre instance [!DNL Veeva CRM]. |
| `auth.params.username` | Valeur du nom d’utilisateur de votre compte [!DNL Veeva CRM]. |
| `auth.params.password` | Valeur du mot de passe de votre compte [!DNL Veeva CRM]. |
| `auth.params.securityToken` | Jeton de sécurité de votre instance [!DNL Veeva CRM]. |
| `connectionSpec.id` | Identifiant de spécification de connexion pour [!DNL Veeva CRM] : `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créer un flux de données pour importer des données CRM dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/crm.md)
