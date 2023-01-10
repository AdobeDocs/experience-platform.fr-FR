---
keywords: Experience Platform;accueil;thèmes populaires;veeva crm;Veeva CRM;Veeva
solution: Experience Platform
title: Création d’une connexion de base CRM Veeva à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Veeva CRM à l’aide de l’API Flow Service.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 75%

---

# Créez une connexion de base à [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Veeva CRM] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour une connexion réussie à [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Veeva CRM], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `environmentUrl` | L’URL de votre [!DNL Veeva CRM] instance. |
| `username` | La valeur username de votre [!DNL Veeva CRM] compte . |
| `password` | La valeur du mot de passe de votre [!DNL Veeva CRM] compte . |
| `securityToken` | Jeton de sécurité pour votre [!DNL Veeva CRM] instance. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Veeva CRM] est `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Pour plus d’informations sur ces valeurs, reportez-vous à cette section [[!DNL Veeva CRM] document](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

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
| `auth.params.environmentUrl` | L’URL de votre [!DNL Veeva CRM] instance. |
| `auth.params.username` | La valeur username de votre [!DNL Veeva CRM] compte . |
| `auth.params.password` | La valeur du mot de passe de votre [!DNL Veeva CRM] compte . |
| `auth.params.securityToken` | Jeton de sécurité pour votre [!DNL Veeva CRM] instance. |
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

En suivant ce tutoriel, vous avez créé une [!DNL Veeva CRM] connexion de base à l’aide de [!DNL Flow Service] API. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de gestion de la relation client dans Platform à l’aide du [!DNL Flow Service] API](../../collect/crm.md)
