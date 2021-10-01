---
keywords: Experience Platform;accueil;rubriques populaires;service de flux de connexion de jeux de données;service de flux;connexion au service de flux
solution: Experience Platform
title: Création d’une connexion de base de jeux de données Adobe Experience Platform à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment utiliser l’API Flow Service pour créer une connexion de base de jeux de données à Adobe Experience Platform.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 38%

---

# Créez une connexion de base de jeu de données [!DNL Experience Platform] à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] sert à collecter et à centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge sont connectables.

Pour connecter les données d’une source tierce à [!DNL Platform], une connexion de base de jeu de données doit d’abord être établie.

Ce tutoriel utilise l’API [!DNL Flow Service] pour vous guider tout au long des étapes de création d’une connexion de base de jeu de données.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Guide](../../../xdm/api/getting-started.md) de développement du registre des schémas : Inclut des informations importantes à connaître pour effectuer avec succès des appels vers l’API Schema Registry. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).
* [Service de catalogue](../../../catalog/home.md) : système d’enregistrement de l’emplacement et de la traçabilité des données dans [!DNL Experience Platform].
* [Ingestion par lots](../../../ingestion/batch-ingestion/overview.md) : L’API d’ingestion par lots vous permet d’ingérer des données dans Experience Platform en tant que fichiers de lot.
* [Environnements de test](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter au lac de données à l’aide de l’API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Recherche des spécifications de connexion

La première étape de la création d’une connexion de base de jeu de données consiste à récupérer un ensemble de spécifications de connexion dans [!DNL Flow Service].

**Format d&#39;API**

Chaque source disponible possède son propre ensemble de spécifications de connexion pour décrire les propriétés du connecteur, telles que les exigences d’authentification. Vous pouvez rechercher les spécifications de connexion pour une connexion de base de jeux de données en exécutant une requête de GET et en utilisant des paramètres de requête.

L’envoi d’une demande de GET sans paramètres de requête renvoie des spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure la requête `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` pour obtenir des informations sur la connexion de base de votre jeu de données.

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

Une réponse réussie renvoie les spécifications de connexion et l’identifiant unique (`id`) requis pour créer une connexion de base.

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

## Création d’une connexion de base de jeu de données

Une connexion de base spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion de base de jeu de données est requise, car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer différentes données.

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
| `connectionSpec.id` | La spécification de connexion `id` récupérée à l’étape précédente. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion de base que vous venez de créer, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour créer une connexion cible et ingérer des données à partir d’un connecteur source tiers.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion de base de jeu de données à l’aide de l’API [!DNL Flow Service] et obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cette connexion de base pour créer une connexion cible. Les tutoriels suivants décrivent les étapes de création d’une connexion cible, en fonction de la catégorie de connecteur source que vous utilisez :

* [Stockage dans le cloud](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Succès des clients](./collect/customer-success.md)
* [Base de données](./collect/database-nosql.md)
