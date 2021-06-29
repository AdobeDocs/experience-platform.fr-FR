---
keywords: Experience Platform;accueil;thèmes populaires;veeva crm;Veeva CRM;Veeva
solution: Experience Platform
title: Création d’une connexion de base CRM Veeva à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Veeva CRM à l’aide de l’API Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 9bd241d5f986759268edd072cee72d02f40f858f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 11%

---

# (Version bêta) Créez une connexion de base [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>La source [!DNL Veeva CRM] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Veeva CRM] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d&#39;Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous avez besoin pour vous connecter à [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Veeva CRM], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `environmentUrl` | URL de votre instance [!DNL Veeva CRM]. |
| `username` | Valeur du nom d’utilisateur de votre compte [!DNL Veeva CRM]. |
| `password` | Valeur du mot de passe de votre compte [!DNL Veeva CRM]. |
| `securityToken` | Jeton de sécurité pour votre instance [!DNL Veeva CRM]. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Veeva CRM] est : `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Pour plus d’informations sur ces valeurs, consultez ce [[!DNL Veeva CRM] document](https://developer.veevacrm.com/api/#order-management-rest-api).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Veeva CRM] dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Veeva CRM] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nom de votre connexion de base [!DNL Veeva CRM]. Vous pouvez utiliser ce nom pour rechercher votre connexion de base [!DNL Veeva CRM]. |
| `description` | Description facultative de votre connexion de base [!DNL Veeva CRM]. |
| `auth.specName` | Type d’authentification utilisé pour la connexion. |
| `auth.params.environmentUrl` | URL de votre instance [!DNL Veeva CRM]. |
| `auth.params.username` | Valeur du nom d’utilisateur de votre compte [!DNL Veeva CRM]. |
| `auth.params.password` | Valeur du mot de passe de votre compte [!DNL Veeva CRM]. |
| `auth.params.securityToken` | Jeton de sécurité pour votre instance [!DNL Veeva CRM]. |
| `connectionSpec.id` | L’identifiant de spécification de connexion pour [!DNL Veeva CRM] : `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est requis à l’étape suivante pour créer une connexion source.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion de base [!DNL Veeva CRM] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer les systèmes de gestion de la relation client à l’aide de l’API Flow Service](../../explore/crm.md).
