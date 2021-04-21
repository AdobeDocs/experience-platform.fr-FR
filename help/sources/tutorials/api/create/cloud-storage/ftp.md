---
keywords: Experience Platform ; accueil ; sujets populaires ; Protocole de transfert de fichiers ; protocole de transfert de fichiers
solution: Experience Platform
title: Création d’une connexion à la source FTP à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à un serveur FTP (File Transfer Protocol) à l’aide de l’API Flow Service.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 26%

---

# Créez une connexion à la source FTP à l’aide de l’API [!DNL Flow Service]

>[!NOTE]
>
>Le connecteur FTP est en version bêta. Les fonctionnalités et la documentation peuvent faire l’objet de changements. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de connexion de [!DNL Experience Platform] à un serveur FTP (File Transfer Protocol).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à un serveur FTP à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] se connecte à FTP, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Nom ou adresse IP associé à votre serveur FTP. |
| `username` | Nom d’utilisateur ayant accès à votre serveur FTP. |
| `password` | mot de passe de votre serveur FTP. |

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte FTP car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

### Création d’une connexion FTP à l’aide d’une authentification de base

Pour créer une connexion FTP à l&#39;aide de l&#39;authentification de base, faites une demande de POST à l&#39;API [!DNL Flow Service] tout en fournissant des valeurs pour les `host`, `userName` et `password` de votre connexion.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion FTP, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour FTP est `fb2e94c9-c031-467d-8103-6bd6e0a432f2`.

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
| `auth.params.password` | mot de passe associé à votre serveur FTP. |
| `connectionSpec.id` | ID de spécification de connexion au serveur FTP : `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la connexion nouvellement créée. Cet identifiant est nécessaire pour explorer votre serveur FTP dans le didacticiel suivant.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion FTP à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet ID de connexion pour [explorer les enregistrements de cloud à l’aide de l’API Flow Service](../../explore/cloud-storage.md) ou [assimiler des données Parquet à l’aide de l’API Flow Service](../../cloud-storage-parquet.md).
