---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de flux de connexion de dataset ; service de flux ; connexion au service de flux
solution: Experience Platform
title: Création d’une connexion de base de données Adobe Experience Platform à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment utiliser l’API du service de flux pour créer une connexion de base de jeux de données à Adobe Experience Platform.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 30%

---

# Créez une connexion de base de jeux de données [!DNL Experience Platform] à l’aide de l’API [!DNL Flow Service].

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Pour connecter les données d&#39;une source tierce à [!DNL Platform], une connexion de base de jeux de données doit d&#39;abord être établie.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de création d&#39;une connexion de base de jeux de données.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Guide](../../../xdm/api/getting-started.md) du développeur du registre des schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [Service de catalogue](../../../catalog/home.md) : système d’enregistrement de l’emplacement et de la traçabilité des données dans [!DNL Experience Platform].
* [Importation](../../../ingestion/batch-ingestion/overview.md) par lot : L’API d’assimilation par lot vous permet d’assimiler des données à des fichiers de commandes dans un Experience Platform.
* [Sandbox](../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à Data Lake à l&#39;aide de l&#39;API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Rechercher les spécifications de connexion

La première étape de la création d&#39;une connexion de base de jeux de données consiste à récupérer un ensemble de spécifications de connexion dans [!DNL Flow Service].

**Format d’API**

Chaque source disponible possède son propre ensemble de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d&#39;authentification. Vous pouvez rechercher des spécifications de connexion pour une connexion de base de jeux de données en exécutant une demande de GET et en utilisant des paramètres de requête.

L&#39;envoi d&#39;une demande de GET sans paramètres de requête retournera des spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure la requête `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` pour obtenir des informations sur votre connexion de base de jeux de données.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Requête**

La requête suivante récupère les spécifications de connexion pour une connexion de base de jeux de données.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les spécifications de connexion et l&#39;identifiant unique (`id`) requis pour créer une connexion de base.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Créer une connexion de base de jeux de données

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base de jeux de données est requise, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| ------------- | --------------- |
| `connectionSpec.id` | Spécification de connexion `id` récupérée à l&#39;étape précédente. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour créer une connexion de cible et assimiler des données à partir d’un connecteur source tiers.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion de base de données à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cette connexion de base pour créer une connexion de cible. Les didacticiels suivants décrivent les étapes de création d’une connexion de cible, en fonction de la catégorie du connecteur source que vous utilisez :

* [Enregistrement cloud](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Réussite des clients](./collect/customer-success.md)
* [Base de données](./collect/database-nosql.md)
