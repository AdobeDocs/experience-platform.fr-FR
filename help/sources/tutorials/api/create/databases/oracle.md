---
keywords: Experience Platform;accueil;rubriques les plus consultées;Oracle;oracle
solution: Experience Platform
title: Création d’une connexion de base d’Oracle à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Oracle à Experience Platform à l’aide de l’API Flow Service.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 12%

---

# Créez une connexion de base [!DNL Oracle] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Oracle] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Oracle] à l’aide de l’API [!DNL Flow Service].

| Credential | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à [!DNL Oracle]. Le modèle de chaîne de connexion [!DNL Oracle] est le suivant : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Oracle] est `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Pour plus d’informations sur la prise en main, consultez ce [[!DNL Oracle] document](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199).

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer des appels avec succès vers les API Platform, consultez le guide de [prise en main des API Platform](../../../../../landing/api-guide.md).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Oracle] dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Oracle] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle connection",
        "description": "A connection for Oracle",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                    "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à votre base de données [!DNL Oracle]. Le modèle de chaîne de connexion [!DNL Oracle] est le suivant : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Oracle] : `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion [!DNL Oracle] à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer les bases de données à l’aide de l’API Flow Service](../../explore/database-nosql.md).
