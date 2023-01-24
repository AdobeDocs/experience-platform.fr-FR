---
title: Création d’une connexion de base SFTP à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à un serveur SFTP (protocole de transfert de fichiers sécurisé) à l’aide de l’API Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 30%

---

# Créez une connexion de base SFTP à l’aide de la variable [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL SFTP] (Protocole de transfert de fichiers sécurisé) à l’aide de la méthode [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

>[!IMPORTANT]
>
>Il est recommandé d’éviter les nouvelles lignes ou les retours chariot lors de l’ingestion d’objets JSON avec une [!DNL SFTP] connexion source. Pour contourner cette limitation, utilisez un seul objet JSON par ligne et plusieurs lignes pour les fichiers qui s’ensuivent.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à un [!DNL SFTP] à l’aide du [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL SFTP], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Le nom ou l’adresse IP associé à votre [!DNL SFTP] serveur. |
| `port` | Port du serveur SFTP auquel vous vous connectez. Si elle n’est pas fournie, la valeur est définie par défaut sur `22`. |
| `username` | Le nom d’utilisateur ayant accès à votre [!DNL SFTP] serveur. |
| `password` | Le mot de passe de votre [!DNL SFTP] serveur. |
| `privateKeyContent` | Contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé en tant que RSA ou DSA. |
| `passPhrase` | L’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si la variable `privateKeyContent` est protégé par mot de passe, ce paramètre doit être utilisé avec comme valeur le mot de passe du contenu de clé privée. |
| `maxConcurrentConnections` | Ce paramètre vous permet de spécifier une limite maximale pour le nombre de connexions simultanées que Platform va créer lors de la connexion à votre serveur SFTP. Vous devez définir cette valeur sur une valeur inférieure à la limite définie par SFTP. **Remarque**: Lorsque ce paramètre est activé pour un compte SFTP existant, il n’affecte que les flux de données futurs et non les flux de données existants. |
| `folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. [!DNL SFTP] source, vous pouvez indiquer le chemin du dossier pour spécifier l’accès de l’utilisateur au sous-dossier de votre choix. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL SFTP] est `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Le [!DNL SFTP] source prend en charge l’authentification et l’authentification de base via la clé publique SSH. Au cours de cette étape, vous pouvez également désigner le chemin d’accès au sous-dossier auquel vous souhaitez accorder l’accès.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL SFTP] dans le cadre des paramètres de requête.

>[!IMPORTANT]
>
>Le [!DNL SFTP] Le connecteur prend en charge une clé OpenSSH de type RSA ou DSA. Assurez-vous que le contenu de votre fichier clé commence par `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` et se termine par `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est un fichier au format PPK, utilisez l’outil PuTTY pour effectuer une conversion de PPK au format OpenSSH.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL SFTP] :

>[!BEGINTABS]

>[!TAB Authentification de base]

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.port` | Port du serveur SFTP. Cette valeur entière est définie par défaut sur 22. |
| `auth.params.username` | Nom d’utilisateur associé à votre serveur SFTP. |
| `auth.params.password` | mot de passe associé à votre serveur SFTP. |
| `auth.params.maxConcurrentConnections` | Nombre maximal de connexions simultanées spécifiées lors de la connexion de Platform à SFTP. Lorsqu’elle est activée, cette valeur doit être définie sur au moins 1. |
| `auth.params.folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |
| `connectionSpec.id` | L’identifiant de spécification de connexion au serveur SFTP : `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB Authentification de clé publique SSH]

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.port` | Port du serveur SFTP. Cette valeur entière est définie par défaut sur 22. |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL SFTP] serveur. |
| `auth.params.privateKeyContent` | Contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé en tant que RSA ou DSA. |
| `auth.params.passPhrase` | L’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par mot de passe, ce paramètre doit être utilisé avec comme valeur le mot de passe de PrivateKeyContent. |
| `auth.params.maxConcurrentConnections` | Nombre maximal de connexions simultanées spécifiées lors de la connexion de Platform à SFTP. Lorsqu’elle est activée, cette valeur doit être définie sur au moins 1. |
| `auth.params.folderPath` | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |
| `connectionSpec.id` | Le [!DNL SFTP] identifiant de spécification de connexion au serveur : `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion Cet identifiant est nécessaire pour explorer votre serveur SFTP dans le tutoriel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL SFTP] connexion à l’aide de la fonction [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion pour [explorer le stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
