---
keywords: Experience Platform;accueil;rubriques les plus consultées ; Protocole de transfert de fichiers; protocole de transfert de fichiers
solution: Experience Platform
title: Création d’une connexion de base FTP à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un serveur FTP (protocole de transfert de fichiers) à l’aide de l’API Flow Service.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 59%

---

# Créez une connexion de base FTP à l’aide de la variable [!DNL Flow Service] API

>[!NOTE]
>
>Le connecteur FTP est en version bêta. Les fonctionnalités et la documentation peuvent faire l’objet de changements. Voir la [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL FTP] (protocole de transfert de fichiers) à l’aide de la méthode [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à un [!DNL FTP] à l’aide du [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL FTP], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Le nom ou l’adresse IP associé à votre [!DNL FTP] serveur. |
| `username` | Le nom d’utilisateur ayant accès à votre [!DNL FTP] serveur. |
| `password` | Le mot de passe de votre [!DNL FTP] serveur. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL FTP] est `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL FTP] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL FTP] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.host` | Nom d’hôte de votre serveur FTP. |
| `auth.params.username` | Nom d’utilisateur associé à votre serveur FTP. |
| `auth.params.password` | mot de passe associé à votre serveur FTP. |
| `connectionSpec.id` | L’identifiant de spécification de connexion au serveur FTP : `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion Cet identifiant est nécessaire pour explorer votre serveur FTP dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion FTP à l’aide de la variable [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion pour [explorer le stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
