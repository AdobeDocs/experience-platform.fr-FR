---
title: Créer une connexion de base SFTP à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un serveur SFTP (Secure File Transfer Protocol) à l’aide de l’API Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 14%

---

# Créer une connexion de base SFTP à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion de base pour [!DNL SFTP] (Secure File Transfer Protocol) à l’aide de l’API [[!DNL Flow Service] ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

>[!IMPORTANT]
>
>Il est recommandé d’éviter les nouvelles lignes ou les retours à la ligne lors de l’ingestion d’objets JSON avec une connexion source [!DNL SFTP]. Pour contourner cette limitation, utilisez un seul objet JSON par ligne et utilisez des lignes multiples pour les fichiers suivants.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir la connexion à un serveur [!DNL SFTP] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez le [[!DNL SFTP] guide d’authentification](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) pour obtenir des instructions détaillées sur la manière de récupérer vos informations d’authentification.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL SFTP]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

La source [!DNL SFTP] prend en charge l’authentification de base et l’authentification par clé publique SSH. Au cours de cette étape, vous pouvez également désigner le chemin d’accès au sous-dossier auquel vous souhaitez accorder l’accès.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL SFTP] dans le cadre des paramètres de requête.

>[!IMPORTANT]
>
>Le connecteur [!DNL SFTP] prend en charge une clé OpenSSH de type RSA ou DSA. Assurez-vous que le contenu de votre fichier clé commence par `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` et se termine par `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est un fichier au format PPK, utilisez l’outil PuTTY pour convertir le fichier PPK au format OpenSSH.

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Authentification de base ]

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.port` | Port du serveur SFTP. Cette valeur entière est 22 par défaut. |
| `auth.params.username` | Nom d’utilisateur associé à votre serveur SFTP. |
| `auth.params.password` | Mot de passe associé à votre serveur SFTP. |
| `auth.params.maxConcurrentConnections` | Nombre maximal de connexions simultanées spécifié lors de la connexion d’Experience Platform au protocole SFTP. Lorsqu’elle est activée, cette valeur doit être définie sur au moins 1. |
| `auth.params.folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |
| `auth.params.disableChunking` | Valeur booléenne utilisée pour déterminer si votre serveur SFTP prend en charge le découpage. |
| `connectionSpec.id` | Identifiant de spécification de connexion au serveur SFTP : `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Réponse

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion nouvellement créée. Cet identifiant est requis pour explorer votre serveur SFTP dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB authentification par clé publique SSH]

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.host` | Nom d’hôte de votre serveur [!DNL SFTP]. |
| `auth.params.port` | Port du serveur SFTP. Cette valeur entière est 22 par défaut. |
| `auth.params.username` | Nom d’utilisateur associé à votre serveur [!DNL SFTP]. |
| `auth.params.privateKeyContent` | Contenu de clé privée SSH codé en Base64. Le type de clé OpenSSH doit être classé comme RSA ou DSA. |
| `auth.params.passPhrase` | Le mot de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par un mot de passe. Si PrivateKeyContent est protégé par mot de passe, ce paramètre doit être utilisé avec la phrase secrète de PrivateKeyContent comme valeur. |
| `auth.params.maxConcurrentConnections` | Nombre maximal de connexions simultanées spécifié lors de la connexion d’Experience Platform au protocole SFTP. Lorsqu’elle est activée, cette valeur doit être définie sur au moins 1. |
| `auth.params.folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |
| `auth.params.disableChunking` | Valeur booléenne utilisée pour déterminer si votre serveur SFTP prend en charge le découpage. |
| `connectionSpec.id` | Identifiant de spécification de connexion au serveur [!DNL SFTP] : `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Réponse

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion nouvellement créée. Cet identifiant est requis pour explorer votre serveur SFTP dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion [!DNL SFTP] à l’aide de l’API [!DNL Flow Service] et d’obtenir la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion pour [explorer les espaces de stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
