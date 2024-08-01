---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point d’entrée de lʼAPI Labels
description: Découvrez la façon de gérer les libellés dʼutilisation des données dans Experience Platform à lʼaide de lʼAPI Policy Service.
role: Developer
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 77d68a42b16c78cdc2b55f7776ba1c8ec98d8acd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 89%

---

# Point d’entrée des libellés

Les libellés dʼutilisation des données vous permettent de classer les données en fonction des politiques dʼutilisation qui peuvent sʼappliquer à ces données. Le point d’entrée `/labels` dans [!DNL Policy Service API] vous permet de gérer par programme les libellés dʼutilisation des données dans votre application Experience.

>[!NOTE]
>
>Le point d’entrée `/labels` nʼest utilisé que pour la récupération, la création et la mise à jour des étiquettes dʼutilisation des données. Vous ne pouvez pas supprimer de libellés. Cependant, vous pouvez ajouter ou supprimer des libellés aux jeux de données et aux champs à l’aide d’appels API. Pour obtenir des instructions, reportez-vous au guide sur la [gestion des libellés de jeux de données](../labels/dataset-api.md) .

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Récupération dʼune liste dʼétiquettes {#list}

Vous pouvez répertorier toutes les étiquettes `core` ou `custom` en réalisant une requête GET à `/labels/core` ou `/labels/custom`, respectivement.

**Format d’API**

```http
GET /labels/core
GET /labels/custom
```

**Requête**

La requête suivante répertorie toutes les étiquettes personnalisées créées dans votre organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste dʼétiquettes personnalisées récupérées du système. Étant donné que lʼexemple de requête ci-dessus a été envoyé à `/labels/custom`, la réponse ci-dessous nʼaffiche que les étiquettes personnalisées.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Recherche dʼune étiquette {#look-up}

Vous pouvez rechercher une étiquette spécifique en incluant la propriété `name` de cette étiquette dans le chemin dʼune requête GET à lʼAPI [!DNL Policy Service].

**Format d’API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | La propriété `name` de lʼétiquette personnalisée que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère lʼétiquette personnalisée `L2`, comme indiqué dans le chemin.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de lʼétiquette personnalisée.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Création ou mise à jour dʼune étiquette personnalisée {#create-update}

Pour créer ou mettre à jour une étiquette personnalisée, vous devez envoyer une requête PUT à lʼAPI [!DNL Policy Service].

>[!NOTE]
>
>Si vous souhaitez supprimer des libellés d’un jeu de données, vous pouvez exécuter une [requête de PUT sur l’API du service de jeux de données](../labels/dataset-api.md#remove) ou à l’aide de l’[interface utilisateur des jeux de données](../labels/user-guide.md#remove-labels-from-a-dataset).

**Format d’API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | Propriété `name` dʼune étiquette personnalisée. Si aucune étiquette personnalisée portant ce nom nʼexiste, une nouvelle étiquette est créée. Sʼil en existe une, cette étiquette sera mise à jour. |

**Requête**

La requête suivante crée une nouvelle étiquette, `L3`, qui vise à décrire les données contenant des informations relatives aux plans de paiement choisis par les clients.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant de chaîne unique pour lʼétiquette. Cette valeur est utilisée à des fins de recherche et dʼapplication de lʼétiquette aux jeux de données et aux champs. Il est donc recommandé quʼelle soit courte et concise. |
| `category` | Catégorie de lʼétiquette. Bien que vous puissiez créer vos propres catégories pour les étiquettes personnalisées, il est vivement recommandé dʼutiliser `Custom` si vous souhaitez que lʼétiquette apparaisse dans lʼinterface utilisateur. |
| `friendlyName` | Nom convivial de lʼétiquette, utilisé pour lʼaffichage. |
| `description` | (Facultatif) Description de lʼétiquette afin de fournir un contexte plus détaillé. |

**Réponse**

Une réponse réussie renvoie les détails de lʼétiquette personnalisée, avec le code HTTP 200 (OK) si une étiquette existante a été mise à jour, ou 201 (Created) si une nouvelle étiquette a été créée.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Étapes suivantes

Ce guide couvre lʼutilisation du point d’entrée `/labels` dans lʼAPI Policy Service. Pour obtenir des instructions détaillées sur lʼapplication dʼétiquettes aux jeux de données et aux champs, consultez le [guide de lʼAPI des étiquettes des jeux de données](../labels/dataset-api.md).
