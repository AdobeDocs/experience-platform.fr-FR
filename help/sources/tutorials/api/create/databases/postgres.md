---
keywords: Experience Platform;accueil;rubriques les plus consultées;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Création d’une connexion de base PostgreSQL à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à PostgreSQL à l’aide de l’API Flow Service.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 54%

---

# Créez une connexion de base à [!DNL PostgreSQL] à l’aide de l’API [!DNL Flow Service].

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes de création dʼune connexion de base pour [!DNL PostgreSQL] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL PostgreSQL] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL PostgreSQL], vous devez fournir la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion associée à votre compte [!DNL PostgreSQL]. Le modèle de chaîne de connexion [!DNL PostgreSQL] est : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’ID de spécification de connexion pour [!DNL PostgreSQL] est `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Pour plus d&#39;informations sur l&#39;obtention d&#39;une chaîne de connexion, consultez ce [[!DNL PostgreSQL] document](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Activer le chiffrement SSL pour votre chaîne de connexion

Vous pouvez activer le cryptage SSL pour votre chaîne de connexion [!DNL PostgreSQL] en ajoutant votre chaîne de connexion avec les propriétés suivantes :

| Propriété | Description | Exemple |
| --- | --- | --- |
| `EncryptionMethod` | Permet d&#39;activer le cryptage SSL sur vos données [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Désactivé)</li><li>`EncryptionMethod=1`(Activé)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valide le certificat envoyé par votre base de données [!DNL PostgreSQL] lorsque `EncryptionMethod` est appliqué. | <uL><li>`ValidationServerCertificate=0`(Désactivé)</li><li>`ValidationServerCertificate=1`(Activé)</li></ul> |

Voici un exemple de chaîne de connexion [!DNL PostgreSQL] ajoutée avec le chiffrement SSL : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL PostgreSQL] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL PostgreSQL] :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| ------------- | --------------- |
| `auth.params.connectionString` | Chaîne de connexion associée à votre compte [!DNL PostgreSQL]. Le modèle de chaîne de connexion [!DNL PostgreSQL] est : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Les [!DNL PostgreSQL] identifiants de spécification de connexion : `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion de base nouvellement créée. Cet identifiant est nécessaire pour explorer votre base de données [!DNL PostgreSQL] dans le tutoriel suivant.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion de base de connexion [!DNL PostgreSQL] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
