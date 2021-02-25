---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de flux ; connexions de mise à jour
solution: Experience Platform
title: Mise à jour des connexions à l’aide de l’API du service de flux
topic: aperçu
type: Tutoriel
description: Ce didacticiel décrit les étapes de mise à jour des détails et des informations d’identification d’une connexion à l’aide de l’API de service de flux.
translation-type: tm+mt
source-git-commit: 5187647dfcf82a476bc776bf2b606db228ca70a4
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 31%

---


# Mise à jour des connexions à l’aide de l’API du service de flux

Dans certains cas, il peut être nécessaire de mettre à jour les détails d&#39;une connexion source existante. [!DNL Flow Service] permet d’ajouter, de modifier et de supprimer des détails d’une connexion existante par lot ou en flux continu, y compris son nom, sa description et ses informations d’identification.

Ce didacticiel décrit les étapes de mise à jour des détails et des informations d’identification d’une connexion à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce didacticiel nécessite une connexion existante et un ID de connexion valide. Si vous n&#39;avez pas de connexion existante, sélectionnez votre source de choix dans le [aperçu des sources](../../home.md) et suivez les étapes décrites avant de tenter ce tutoriel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
* [Environnements de test](../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour mettre à jour une connexion à l&#39;aide de l&#39;API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources en Experience Platform, y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Rechercher les détails de connexion

La première étape de la mise à jour de votre connexion consiste à récupérer ses détails à l’aide de votre ID de connexion. Pour récupérer les détails actuels de votre connexion, faites une demande de GET à l&#39;API [!DNL Flow Service] tout en fournissant l&#39;ID de connexion de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` unique pour la connexion que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère les informations relatives à votre connexion.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails actuels de votre connexion, y compris ses informations d&#39;identification, son identifiant unique (`id`) et sa version. La valeur de version est requise pour mettre à jour votre connexion.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Mettre à jour la connexion

Pour mettre à jour le nom, la description et les informations d&#39;identification de votre connexion, effectuez une requête de PATCH à l&#39;API [!DNL Flow Service] tout en fournissant votre ID de connexion, votre version et les nouvelles informations que vous souhaitez utiliser.

>[!IMPORTANT]
>
>L&#39;en-tête `If-Match` est requis lors de l&#39;exécution d&#39;une demande de PATCH. La valeur de cet en-tête est la version unique de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` unique pour la connexion à mettre à jour. |

**Requête**

La requête suivante fournit un nouveau nom et une nouvelle description, ainsi qu’un nouvel ensemble d’informations d’identification, pour mettre à jour votre connexion.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d’accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion et une balise mise à jour. Vous pouvez vérifier la mise à jour en adressant une demande de GET à l&#39;API [!DNL Flow Service], tout en fournissant votre identifiant de connexion.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez mis à jour les informations d’identification et les informations associées à votre connexion à l’aide de l’API [!DNL Flow Service]. Pour plus d&#39;informations sur l&#39;utilisation des connecteurs source, consultez l&#39;[aperçu des sources](../../home.md).
