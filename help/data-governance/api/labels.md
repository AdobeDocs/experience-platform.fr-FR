---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point d’entrée de lʼAPI Labels
description: Découvrez la façon de gérer les libellés dʼutilisation des données dans Experience Platform à lʼaide de lʼAPI Policy Service.
role: Developer
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
TQID: https://experienceleague.adobe.com/Qy-H-Grw4eQkt4o3pECd1qL7eSnVulXKFRt1glex1yw
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 543
ht-degree: 88%

---

# Point d’entrée des libellés

Les libellés dʼutilisation des données vous permettent de classer les données en fonction des politiques dʼutilisation qui peuvent sʼappliquer à ces données. Le point d’entrée `/labels` dans [!DNL Policy Service API] vous permet de gérer par programme les libellés dʼutilisation des données dans votre application Experience.

>[!NOTE]
>
>Le point d’entrée `/labels` nʼest utilisé que pour la récupération, la création et la mise à jour des libellés dʼutilisation des données. Vous ne pouvez pas supprimer les libellés. Cependant, vous pouvez ajouter ou supprimer des libellés aux jeux de données et aux champs à l’aide d’appels API. Reportez-vous au guide sur le document [gestion des libellés de jeu de données](../labels/dataset-api.md) pour obtenir des instructions.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Policy Service API]](https://developer.adobe.com/experience-platform-apis/references/policy-service). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Récupération dʼune liste de libellés {#list}

Vous pouvez répertorier tous les libellés `core` ou `custom` en réalisant une requête GET à `/labels/core` ou `/labels/custom`, respectivement.

**Format d’API**

```http
GET /labels/core
GET /labels/custom
```

**Requête**

La requête suivante répertorie tous les libellés personnalisés créés dans votre organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de libellés personnalisés récupérés du système. Étant donné que lʼexemple de requête ci-dessus a été envoyé à `/labels/custom`, la réponse ci-dessous nʼaffiche que les libellés personnalisés.

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

## Recherche dʼun libellé {#look-up}

Vous pouvez rechercher un libellé spécifique en incluant la propriété `name` de ce libellé dans le chemin dʼune requête GET à lʼAPI [!DNL Policy Service].

**Format d’API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | La propriété `name` du libellé personnalisé que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère le libellé personnalisé `L2`, comme indiqué dans le chemin.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails du libellé personnalisé.

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

## Création ou mise à jour dʼun libellé personnalisé {#create-update}

Pour créer ou mettre à jour un libellé personnalisé, vous devez envoyer une requête PUT à lʼAPI [!DNL Policy Service].

>[!NOTE]
>
>Si vous souhaitez supprimer des libellés d’un jeu de données, vous pouvez effectuer une requête [PUT sur l’API Dataset Service](../labels/dataset-api.md#remove) ou utiliser l’interface utilisateur [Datasets](../labels/user-guide.md#remove-labels-from-a-dataset).

**Format d’API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{LABEL_NAME}` | Propriété `name` dʼun libellé personnalisé. Si aucun libellé personnalisé portant ce nom nʼexiste, un nouveau libellé est créé. Sʼil en existe un, ce libellé sera mis à jour. |

**Requête**

La requête suivante crée un nouveau libellé, `L3`, qui vise à décrire les données contenant des informations relatives aux plans de paiement choisis par les clientes et les clients.

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
| `name` | Identifiant de chaîne unique pour le libellé. Cette valeur est utilisée à des fins de recherche et dʼapplication du libellé aux jeux de données et aux champs. Il est donc recommandé quʼelle soit courte et concise. |
| `category` | Catégorie du libellé. Bien que vous puissiez créer vos propres catégories pour les libellés personnalisés, il est vivement recommandé dʼutiliser `Custom` si vous souhaitez que le libellé apparaisse dans lʼinterface utilisateur. |
| `friendlyName` | Nom convivial du libellé, utilisé pour lʼaffichage. |
| `description` | (Facultatif) Description du libellé afin de fournir un contexte plus détaillé. |

**Réponse**

Une réponse réussie renvoie les détails du libellé personnalisé, avec le code HTTP 200 (OK) si un libellé existant a été mis à jour, ou 201 (Created) si un nouveau libellé a été créé.

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

Ce guide couvre lʼutilisation du point d’entrée `/labels` dans lʼAPI Policy Service. Pour obtenir des instructions détaillées sur lʼapplication de libellés aux jeux de données et aux champs, consultez le [guide de lʼAPI des libellés des jeux de données](../labels/dataset-api.md).
