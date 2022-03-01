---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;mettre à jour des comptes
solution: Experience Platform
title: Mise à jour des comptes à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour mettre à jour les détails et les informations d’identification d’un compte à l’aide de l’API Flow Service.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 15%

---

# Mise à jour de comptes à l’aide de l’API Flow Service

Dans certains cas, il peut être nécessaire de mettre à jour les détails d’une connexion source existante. [!DNL Flow Service] vous permet d’ajouter, de modifier et de supprimer les détails d’un lot ou d’une connexion en continu existante, y compris son nom, sa description et ses informations d’identification.

Ce tutoriel décrit les étapes à suivre pour mettre à jour les détails et les informations d’identification d’une connexion à l’aide de la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce tutoriel nécessite que vous disposiez d’une connexion existante et d’un identifiant de connexion valide. Si vous ne disposez pas d’une connexion existante, sélectionnez votre source de choix dans la [présentation des sources](../../home.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../landing/api-guide.md).

## Recherche des détails de connexion

La première étape de la mise à jour de votre connexion consiste à récupérer ses détails à l’aide de votre identifiant de connexion. Pour récupérer les détails actuels de votre connexion, envoyez une demande de GET à la variable [!DNL Flow Service] API lors de la fourniture de l’identifiant de connexion, de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | L’unique `id` pour la connexion que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations concernant votre connexion.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails actuels de votre connexion, y compris ses informations d’identification et son identifiant unique (`id`), et version. La valeur de version est requise pour mettre à jour votre connexion.

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

Pour mettre à jour le nom, la description et les informations d’identification de votre connexion, envoyez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de votre ID de connexion, de votre version et des nouvelles informations que vous souhaitez utiliser.

>[!IMPORTANT]
>
>Le `If-Match` est requis lors de l’exécution d’une requête de PATCH. La valeur de cet en-tête est la version unique de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | L’unique `id` pour la connexion que vous souhaitez mettre à jour. |

**Requête**

La requête suivante fournit un nouveau nom et une nouvelle description, ainsi qu’un nouveau jeu d’informations d’identification, avec lequel mettre à jour votre connexion.

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
| `op` | Appel d&#39;opération utilisé pour définir l&#39;action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d&#39;accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion et une balise mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à la variable [!DNL Flow Service] de l’API, tout en fournissant votre identifiant de connexion.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez mis à jour les informations d’identification et de connexion associées à votre connexion à l’aide de la variable [!DNL Flow Service] API. Pour plus d’informations sur l’utilisation des connecteurs source, voir [présentation des sources](../../home.md).
