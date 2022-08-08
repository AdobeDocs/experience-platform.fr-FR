---
title: Point d’entrée de l’API de l’ordre de travail
description: Le point d’entrée /workorder de l’API Data Hygiene vous permet de gérer par programmation les tâches de suppression des identités des clients.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: ht
source-wordcount: '998'
ht-degree: 100%

---

# Point d’entrée de l’ordre de travail

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités de nettoyage de données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté Healthcare Shield.

Le point d’entrée `/workorder` de l’API Data Hygiene vous permet de gérer par programmation les tâches de suppression des identités des clients dans Adobe Experience Platform.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de continuer, consultez la [présentation](./overview.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Supprimer des identités {#delete-identities}

Vous pouvez supprimer une ou plusieurs identités de clients d’un seul jeu de données ou de tous les jeux de données en effectuant une requête POST au point d’entrée `/workorder`.

**Format d’API**

```http
POST /workorder
```

**Requête**

En fonction de la valeur de `datasetId` fournie dans le payload de requête, l’appel API supprime les identités des clients de tous les jeux de données ou d’un seul jeu de données que vous spécifiez. La requête suivante supprime trois identités de clients d’un jeu de données spécifique.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `action` | L’action à effectuer. La valeur doit être définie sur `delete_identity` lors de la suppression des identités. |
| `datasetId` | Si vous effectuez une suppression dans un seul jeu de données, cette valeur doit correspondre à l’identifiant du jeu de données en question. Si vous effectuez une suppression dans tous les jeux de données, définissez la valeur sur `ALL`.<br><br>Si vous spécifiez un seul jeu de données, une identité principale doit être définie pour le schéma de modèle de données d’expérience (XDM) associé au jeu de données. |
| `identities` | Un tableau contenant les identités d’au moins un utilisateur dont vous souhaitez supprimer les informations. Chaque identité se compose d’un [espace de noms d’identité](../../identity-service/namespaces.md) et d’une valeur :<ul><li>`namespace` : contient une seule propriété de chaîne, `code`, qui représente l’espace de noms d’identité. </li><li>`id` : la valeur de l’identité.</ul>Si `datasetId` spécifie un seul jeu de données, chaque entité sous `identities` doit utiliser le même espace de noms d’identité que l’identité principale du schéma.<br><br>Si `datasetId` est défini sur `ALL`, le tableau `identities` n’est limité à aucun espace de noms unique, car chaque jeu de données peut être différent. Toutefois, les requêtes sont toujours limitées aux espaces de noms disponibles pour l’organisation, comme indiqué par le [service d’identités](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de la suppression d’identité.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | L’identifiant de l’organisation. |
| `batchId` | L’identifiant du lot auquel cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés dans un lot pour être traités par les services en aval. |
| `bundleOrdinal` | L’ordre dans lequel cet ordre de suppression a été reçu lorsqu’il a été regroupé dans un lot pour un traitement en aval. Utilisé à des fins de débogage. |
| `payloadByteSize` | La taille, en octets, de la liste des identités fournies dans le payload de requête à l’origine de cet ordre de suppression. |
| `operationCount` | Le nombre d’identités auxquelles s’applique cet ordre de suppression. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `responseMessage` | La dernière réponse renvoyée par le système. Si une erreur se produit lors du traitement, cette valeur est une chaîne JSON contenant des informations détaillées sur les erreurs afin de vous aider à comprendre ce qui s’est passé. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |

{style=&quot;table-layout:auto&quot;}

## Répertorier les statuts de toutes les suppressions d’identité {#list}

Vous pouvez répertorier les statuts de toutes les suppressions d’identité en effectuant une requête GET.

**Format d’API**

```http
GET /workorder?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMS}` | Une liste des paramètres de requête facultatifs pour l’appel de liste, avec plusieurs paramètres séparés par des caractères `&`. Les paramètres de requête acceptés sont les suivants :<ul><li>`data` : une valeur booléenne qui, lorsqu’elle est définie sur `true`, comprend toutes les données de requête et de réponse supplémentaires reçues pour l’ordre de suppression. La valeur par défaut est `false`.</li><li>`start` : date et heure de début du délai de recherche des ordres de suppression.</li><li>`end` : date et heure de fin du délai de recherche des ordres de suppression.</li><li>`page` : la page de réponse spécifique à renvoyer.</li><li>`limit` : le nombre d’enregistrements à afficher par page.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de toutes les opérations de suppression, y compris leur statut actuel. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `results` | Contient la liste des ordres de suppression et les détails. Pour plus d’informations sur les propriétés d’un ordre de suppression, consultez l’exemple de réponse dans la section sur la [recherche d’un ordre de suppression](#lookup). |
| `total` | Le nombre total d’ordres de suppression trouvés en fonction des filtres actuels. |
| `count` | Le nombre total d’ordres de suppression trouvés sur chaque page de la réponse. |
| `_links` | Contient des informations de pagination vous permettant de découvrir le reste de la réponse :<ul><li>`next` : contient l’URL de la page suivante dans la réponse.</li><li>`page` : contient un modèle d’URL pour accéder à une autre page de la réponse ou ajuster le nombre d’éléments renvoyés sur chaque page.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Récupérer le statut d’une suppression d’identité (#lookup)

Après avoir envoyé une requête pour [supprimer une identité](#delete-identities), vous pouvez vérifier son statut à l’aide d’une requête GET.

**Format d’API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | Le `workorderId` de la suppression d’identité que vous recherchez. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’opération de suppression, y compris son statut actuel.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | L’identifiant de l’organisation. |
| `batchId` | L’identifiant du lot auquel cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés dans un lot pour être traités par les services en aval. |
| `bundleOrdinal` | L’ordre dans lequel cet ordre de suppression a été reçu lorsqu’il a été regroupé dans un lot pour un traitement en aval. Utilisé à des fins de débogage. |
| `payloadByteSize` | La taille, en octets, de la liste des identités fournies dans le payload de requête à l’origine de cet ordre de suppression. |
| `operationCount` | Le nombre d’identités auxquelles s’applique cet ordre de suppression. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `responseMessage` | La dernière réponse renvoyée par le système. Si une erreur se produit lors du traitement, cette valeur est une chaîne JSON contenant des informations détaillées sur les erreurs afin de vous aider à comprendre ce qui s’est passé. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
