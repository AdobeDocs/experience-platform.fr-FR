---
keywords: Experience Platform ; accueil ; rubriques populaires ; SFTP ; sftp ; Secure File Transfer Protocol ; protocole de transfert de fichiers sécurisé
solution: Experience Platform
title: Création d’une connexion de base SFTP à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un serveur SFTP (Secure File Transfer Protocol) à l’aide de l’API Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 7%

---

# Créez une connexion de base SFTP à l’aide de la [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous explique les étapes à suivre pour créer une connexion de base pour [!DNL SFTP] (Secure File Transfer Protocol) à l’aide de la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide des services de la plate-forme.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

>[!IMPORTANT]
>
>Il est recommandé d’éviter les nouvelles lignes ou les retours chariot lors de l’assimilation d’objets JSON avec un [!DNL SFTP] connexion source. Pour contourner cette limitation, utilisez un seul objet JSON par ligne et utilisez plusieurs lignes pour les fichiers suivants.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour vous connecter à un [!DNL SFTP] à l’aide de la [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour se connecter à [!DNL SFTP], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| `host` | Le nom ou l’adresse IP associés à votre [!DNL SFTP] serveur. |
| `port` | Le port du serveur SFTP auquel vous vous connectez. Si elle n’est pas fournie, la valeur est définie par défaut sur `22`. |
| `username` | Nom d’utilisateur ayant accès à votre [!DNL SFTP] serveur. |
| `password` | Le mot de passe de votre [!DNL SFTP] serveur. |
| `privateKeyContent` | Le contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé comme RSA ou DSA. |
| `passPhrase` | L’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de clé est protégé par une expression de passe. Si la `privateKeyContent` est protégé par mot de passe, ce paramètre doit être utilisé avec la phrase de passe du contenu de clé privée comme valeur. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. ID de spécification de connexion pour [!DNL SFTP] est : `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Utilisation des API de plate-forme

Pour plus d’informations sur la manière d’effectuer des appels vers les API de plate-forme, consultez le guide sur [prise en main des API de plate-forme](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et la plate-forme, y compris les informations d&#39;identification de votre source, l&#39;état actuel de la connexion et votre ID de connexion de base unique. L’ID de connexion de base vous permet d’explorer et de parcourir les fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez assimiler, y compris des informations concernant leurs types et formats de données.

Pour créer un ID de connexion de base, effectuez une demande de POST à l’adresse `/connections` point de terminaison lors de la fourniture de votre [!DNL SFTP] les informations d&#39;identification d&#39;authentification dans le cadre des paramètres de demande.

### Créer un [!DNL SFTP] connexion de base à l&#39;aide de l&#39;authentification de base

Pour créer un [!DNL SFTP] connexion de base à l’aide de l’authentification de base, effectuez une demande de POST à l’adresse suivante : [!DNL Flow Service] API tout en fournissant des valeurs pour votre connexion `host`, `userName`et `password`.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL SFTP] à l&#39;aide de l&#39;authentification de base :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.host` | Nom d’hôte de votre serveur SFTP. |
| `auth.params.username` | Nom d’utilisateur associé à votre serveur SFTP. |
| `auth.params.password` | Mot de passe associé à votre serveur SFTP. |
| `connectionSpec.id` | ID de spécification de connexion de serveur SFTP : `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion nouvellement créée. Cet ID est nécessaire pour explorer votre serveur SFTP dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Créer un [!DNL SFTP] connexion de base à l&#39;aide de l&#39;authentification à clé publique SSH

Pour créer un [!DNL SFTP] connexion de base à l’aide de l’authentification de clé publique SSH, effectuez une demande de POST à l’adresse suivante : [!DNL Flow Service] API tout en fournissant des valeurs pour votre connexion `host`, `userName`, `privateKeyContent`et `passPhrase`.

>[!IMPORTANT]
>
>Le [!DNL SFTP] connecteur prend en charge une clé OpenSSH de type RSA ou DSA. Assurez-vous que le contenu de votre fichier clé commence par `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` et se termine par `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est au format PPK, utilisez l’outil PuTTY pour convertir le fichier de clé privée au format OpenSSH.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL SFTP] à l&#39;aide de l&#39;authentification à clé publique SSH :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.host` | Le nom d’hôte de votre [!DNL SFTP] serveur. |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL SFTP] serveur. |
| `auth.params.privateKeyContent` | Le contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé comme RSA ou DSA. |
| `auth.params.passPhrase` | L’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par un mot de passe, ce paramètre doit être utilisé avec la phrase de passe de PrivateKeyContent comme valeur. |
| `connectionSpec.id` | Le [!DNL SFTP] ID de spécification de connexion de serveur : `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion nouvellement créée. Cet ID est nécessaire pour explorer votre [!DNL SFTP] dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un fichier [!DNL SFTP] connexion à l’aide de la [!DNL Flow Service] et ont obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet ID de connexion pour [exploration des sites de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
