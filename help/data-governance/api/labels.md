---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API Libellés
topic-legacy: developer guide
description: Découvrez comment gérer les étiquettes d’utilisation des données dans l’Experience Platform à l’aide de l’API Policy Service.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 6%

---

# Point de terminaison des étiquettes

Les étiquettes d’utilisation des données vous permettent de classer les données en fonction des stratégies d’utilisation qui peuvent s’appliquer à ces données. Le point de terminaison `/labels` dans [!DNL Policy Service API] vous permet de gérer par programmation les étiquettes d’utilisation des données dans votre application d’expérience.

>[!NOTE]
>
>Le point de terminaison `/labels` n&#39;est utilisé que pour récupérer, créer et mettre à jour des étiquettes d&#39;utilisation des données. Pour savoir comment ajouter des libellés aux jeux de données et aux champs à l’aide d’appels d’API, consultez le guide [gestion des libellés de jeux de données](../labels/dataset-api.md).

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie du [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API [!DNL Experience Platform].

## Récupérer une liste d&#39;étiquettes {#list}

Vous pouvez liste toutes les étiquettes `core` ou `custom` en adressant une demande de GET à `/labels/core` ou `/labels/custom`, respectivement.

**Format d’API**

```http
GET /labels/core
GET /labels/custom
```

**Requête**

La requête suivante liste tous les libellés personnalisés créés dans votre organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d&#39;étiquettes personnalisées récupérées du système. Comme l&#39;exemple de demande ci-dessus a été envoyé à `/labels/custom`, la réponse ci-dessous n&#39;affiche que les étiquettes personnalisées.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Rechercher une étiquette {#look-up}

Vous pouvez rechercher une étiquette spécifique en incluant la propriété `name` de cette étiquette dans le chemin d&#39;une demande de GET à l&#39;API [!DNL Policy Service].

**Format d’API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | La propriété `name` du libellé personnalisé que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère le libellé personnalisé `L2`, comme indiqué dans le chemin d’accès.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’étiquette personnalisée.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
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

## Créer ou mettre à jour une étiquette personnalisée {#create-update}

Pour créer ou mettre à jour une étiquette personnalisée, vous devez envoyer une requête de PUT à l&#39;API [!DNL Policy Service].

**Format d’API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | Propriété `name` d’une étiquette personnalisée. Si aucune étiquette personnalisée portant ce nom n’existe, une nouvelle étiquette est créée. S&#39;il en existe un, cette étiquette sera mise à jour. |

**Requête**

La demande suivante crée une nouvelle étiquette, `L3`, qui vise à décrire les données contenant des informations relatives aux plans de paiement sélectionnés par les clients.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Identifiant de chaîne unique pour l’étiquette. Cette valeur est utilisée à des fins de recherche et d’application de l’étiquette aux jeux de données et aux champs. Il est donc recommandé qu’elle soit courte et concise. |
| `category` | Catégorie de l&#39;étiquette. Bien que vous puissiez créer vos propres catégories pour les étiquettes personnalisées, il est vivement recommandé d’utiliser `Custom` si vous souhaitez que le libellé apparaisse dans l’interface utilisateur. |
| `friendlyName` | Nom convivial de l’étiquette, utilisé à des fins d’affichage. |
| `description` | (Facultatif) Description de l’étiquette afin de fournir un contexte plus poussé. |

**Réponse**

Une réponse réussie renvoie les détails d&#39;une étiquette personnalisée, avec le code HTTP 200 (OK) si une étiquette existante a été mise à jour, ou 201 (Créée) si une nouvelle étiquette a été créée.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

Ce guide traite de l&#39;utilisation du point de terminaison `/labels` dans l&#39;API Policy Service. Pour savoir comment appliquer des libellés aux jeux de données et aux champs, consultez le [guide de l&#39;API des libellés de jeux de données](../labels/dataset-api.md).
