---
keywords: Experience Platform;accueil;rubriques les plus consultées;stockage d’objet Oracle;stockage d’objet oracle
solution: Experience Platform
title: Création d’une connexion de base de stockage d’objets Oracle à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Oracle Object Storage à l’aide de l’API Flow Service.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 50%

---

# Créez un [!DNL Oracle Object Storage] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL Oracle Object Storage] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Oracle Object Storage] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Oracle Object Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUrl` | Le [!DNL Oracle Object Storage] point d’entrée requis pour l’authentification. Le format du point de terminaison est le suivant : `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Le [!DNL Oracle Object Storage] ID de clé d’accès requis pour l’authentification. |
| `secretKey` | Le [!DNL Oracle Object Storage] mot de passe requis pour l’authentification. |
| `bucketName` | Nom du compartiment autorisé requis si l’utilisateur dispose d’un accès restreint. Le nom du compartiment doit comporter entre trois et 63 caractères, il doit commencer et se terminer par une lettre ou un nombre et ne peut contenir que des minuscules lettres, des chiffres ou des tirets (`-`). Le nom du compartiment ne peut pas être formaté comme une adresse IP. |
| `folderPath` | Chemin d’accès au dossier autorisé requis si l’utilisateur dispose d’un accès restreint. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Oracle Object Storage] est `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Pour plus d’informations sur l’obtention de ces valeurs, reportez-vous à la section [Guide d’authentification du stockage d’objets Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Oracle Object Storage] dans les paramètres de la requête.

**Format d’API**

```http
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Oracle Object Storage] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.serviceUrl` | Le [!DNL Oracle Object Storage] point d’entrée requis pour l’authentification. |
| `auth.params.accessKey` | Le [!DNL Oracle Object Storage] ID de clé d’accès requis pour l’authentification. |
| `auth.params.secretKey` | Le [!DNL Oracle Object Storage] mot de passe requis pour l’authentification. |
| `auth.params.bucketName` | Nom du compartiment autorisé requis si l’utilisateur dispose d’un accès restreint. |
| `auth.params.folderPath` | Chemin d’accès au dossier autorisé requis si l’utilisateur dispose d’un accès restreint. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Oracle Object Storage] : `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Réponse**

Une réponse réussie renvoie l’identifiant de connexion de la nouvelle connexion. Cet identifiant est nécessaire pour explorer vos données de stockage dans le cloud dans le tutoriel suivant.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une [!DNL Oracle Object Storage] connexion à l’aide de la fonction [!DNL Flow Service] et ont obtenu son identifiant de connexion unique. Vous pouvez utiliser cet identifiant de connexion pour [explorer le stockage dans le cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
