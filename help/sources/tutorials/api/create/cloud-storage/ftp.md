---
keywords: Experience Platform ; accueil ; sujets populaires ; Protocole de transfert de fichiers ; protocole de transfert de fichiers
solution: Experience Platform
title: Création d'une connexion de base FTP à l'aide de l'API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un serveur FTP (File Transfer Protocol) à l’aide de l’API Flow Service.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 13%

---

# Créez une connexion de base FTP à l’aide de la [!DNL Flow Service] API

>[!NOTE]
>
>Le connecteur FTP est en version bêta. Les fonctionnalités et la documentation peuvent faire l’objet de changements. Voir la section [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés bêta.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous explique les étapes à suivre pour créer une connexion de base pour [!DNL FTP] (Protocole de transfert de fichiers) à l’aide de la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour vous connecter à un [!DNL FTP] à l’aide de la [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour se connecter à [!DNL FTP], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| `host` | Le nom ou l’adresse IP associés à votre [!DNL FTP] serveur. |
| `username` | Nom d’utilisateur ayant accès à votre [!DNL FTP] serveur. |
| `password` | Le mot de passe de votre [!DNL FTP] serveur. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. ID de spécification de connexion pour [!DNL FTP] est : `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Utilisation des API de plate-forme

Pour plus d’informations sur la manière d’effectuer des appels vers les API de plate-forme, consultez le guide sur [prise en main des API de plate-forme](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et la plate-forme, y compris les informations d&#39;identification de votre source, l&#39;état actuel de la connexion et votre ID de connexion de base unique. L’ID de connexion de base vous permet d’explorer et de parcourir les fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez assimiler, y compris des informations concernant leurs types et formats de données.

Pour créer un ID de connexion de base, effectuez une demande de POST à l’adresse `/connections` point de terminaison lors de la fourniture de votre [!DNL FTP] les informations d&#39;identification d&#39;authentification dans le cadre des paramètres de demande.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.password` | Mot de passe associé à votre serveur FTP. |
| `connectionSpec.id` | ID de spécification de connexion de serveur FTP : `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion nouvellement créée. Cet ID est nécessaire pour explorer votre serveur FTP dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion FTP à l’aide de la [!DNL Flow Service] et ont obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet ID de connexion pour [exploration des sites de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
