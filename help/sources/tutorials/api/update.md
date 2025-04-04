---
title: Mettre à jour des comptes à l’aide de l’API Flow Service
description: Ce tutoriel décrit les étapes à suivre pour mettre à jour les détails et les informations d’identification d’un compte à l’aide de l’API Flow Service.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 77%

---

# Mettre à jour des comptes à l’aide de l’API Flow Service

Dans certains cas, il peut être nécessaire de mettre à jour les détails d’une connexion de base existante. [!DNL Flow Service] vous permet d’ajouter, de modifier et de supprimer les détails d’un lot ou d’une connexion de diffusion en continu existante, y compris son nom, sa description et ses informations d’identification.

Ce tutoriel décrit les étapes à suivre pour mettre à jour les détails et les informations d’identification d’une connexion à l’aide de lʼ[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!TIP]
>
>Vous n’avez pas besoin de créer de connexion de base lorsqu’une mise à jour est requise. Toutes les modifications apportées à votre connexion de base sont répercutées dans le flux de données associé.

## Prise en main

Ce tutoriel nécessite que vous disposiez d’une connexion existante et d’un identifiant de connexion valide. Si vous ne disposez pas de connexion existante, sélectionnez la source de votre choix dans la [présentation des sources](../../home.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).

## Rechercher les détails de la connexion

Pour mettre à jour votre connexion, la première étape consiste à récupérer les détails de celle-ci à l’aide de votre identifiant de connexion. Pour récupérer les détails actuels de votre connexion, effectuez une requête GET à lʼAPI [!DNL Flow Service] en fournissant l’identifiant de connexion de la connexion à mettre à jour.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` unique pour la connexion que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations sur votre connexion.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails actuels de votre connexion, y compris ses informations d’identification, son identifiant unique (`id`) et sa version. La valeur de la version est requise pour mettre à jour votre connexion.

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

## Mettre à jour une connexion

Pour mettre à jour le nom, la description et les informations d’identification de votre connexion, envoyez une requête PATCH à l’API [!DNL Flow Service] et fournissez votre identifiant de connexion, la valeur de version et les nouvelles informations que vous souhaitez utiliser.

>[!IMPORTANT]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête PATCH. La valeur de cet en-tête est la version unique de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` unique pour la connexion que vous souhaitez mettre à jour. |

**Requête**

La requête suivante fournit un nouveau nom, une nouvelle description et un nouveau jeu d’informations d’identification, avec lesquels vous allez mettre à jour votre connexion.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie votre identifiant de connexion et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en fournissant votre identifiant de connexion.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Étapes suivantes

Vous êtes arrivé au bout de ce tutoriel, félicitations ! Grâce à celui-ci, vous avez mis à jour les informations d’identification et de connexion associées à votre connexion à l’aide de l’API [!DNL Flow Service]. Pour plus d’informations sur l’utilisation des connecteurs source, consultez la [présentation des sources](../../home.md).
