---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’une connexion de base de jeux de données de plateformes d’expérience à l’aide de l’API de service de flux
topic: overview
translation-type: tm+mt
source-git-commit: e409b287d6965ede4030829287bd3e405e9d709b
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# Création d’une connexion de base de jeux de données de plateformes d’expérience à l’aide de l’API de service de flux

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Pour connecter des données d&#39;une source tierce à la plate-forme, une connexion de base de jeux de données doit d&#39;abord être établie.

Ce didacticiel utilise l’API du service de flux pour vous guider dans les étapes de création d’une connexion de base de jeux de données.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Guide](../../../xdm/api/getting-started.md)du développeur du registre des Schémas : Inclut des informations importantes que vous devez connaître pour pouvoir effectuer des appels à l&#39;API de registre du Schéma. Cela inclut votre `{TENANT_ID}`nom, le concept de &quot;conteneurs&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accepter et à ses valeurs possibles).
* [Service](../../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données dans la plate-forme d’expérience.
* [Importation](../../../ingestion/batch-ingestion/overview.md)par lot : L’API d’assimilation par lot vous permet d’assimiler des données dans la plate-forme d’expérience sous la forme de fichiers par lot.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à Data Lake à l’aide de l’API de service de flux.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Rechercher les spécifications de connexion

La première étape de la création d’une connexion de base de jeux de données consiste à récupérer un ensemble de spécifications de connexion dans le service de flux.

**Format d’API**

Chaque source disponible possède son propre ensemble de spécifications de connexion unique pour décrire les propriétés du connecteur, telles que les exigences d&#39;authentification. Vous pouvez rechercher des spécifications de connexion pour une connexion de base de jeux de données en exécutant une requête GET et en utilisant des paramètres de requête.

L&#39;envoi d&#39;une demande GET sans paramètres de requête retournera les spécifications de connexion pour toutes les sources disponibles. Vous pouvez inclure la requête `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` pour obtenir des informations sur votre connexion de base de jeux de données.

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

En suivant ce didacticiel, vous avez créé une connexion de base de jeux de données à l’aide de l’API Flow Service et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cette connexion de base pour créer une connexion de cible. Les didacticiels suivants décrivent les étapes de création d’une connexion de cible, en fonction de la catégorie du connecteur source que vous utilisez :

* [enregistrement cloud](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Réussite des clients](./collect/customer-success.md)
* [Base de données](./collect/database-nosql.md)