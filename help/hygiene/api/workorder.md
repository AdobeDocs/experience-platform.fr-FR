---
title: Point de terminaison de l’API de l’ordre de travail
description: Le point d’entrée /workorder de l’API Data Hygiene vous permet de gérer par programmation les tâches de suppression pour les identités des consommateurs.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 5%

---

# Point d’entrée de l’ordre de travail

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

Le `/workorder` Le point de terminaison de l’API Data Hygiene vous permet de gérer par programmation les tâches de suppression pour les identités des consommateurs dans Adobe Experience Platform.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’API Data Hygiene. Avant de poursuivre, veuillez consulter la section [aperçu](./overview.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d’appels API de ce document, ainsi que des informations importantes concernant les en-têtes requis pour réussir les appels à une API Experience Platform.

## Suppression d’identités {#delete-identities}

Vous pouvez supprimer une ou plusieurs identités de consommateur d’un seul jeu de données ou de tous les jeux de données en adressant une requête de POST à la variable `/workorder` point de terminaison .

**Format d’API**

```http
POST /workorder
```

**Requête**

Selon la valeur de la variable `datasetId` fourni dans le payload de requête, l’appel API supprime les identités des consommateurs de tous les jeux de données ou d’un seul jeu de données que vous spécifiez. La requête suivante supprime trois identités de consommateur d’un jeu de données spécifique.

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
| `action` | Action à effectuer. La valeur doit être définie sur `delete_identity` lors de la suppression d’identités. |
| `datasetId` | Si vous supprimez d’un seul jeu de données, cette valeur doit correspondre à l’identifiant du jeu de données en question. Si vous supprimez de tous les jeux de données, définissez la valeur sur `ALL`.<br><br>Si vous spécifiez un seul jeu de données, une identité Principale doit être définie pour le schéma de modèle de données d’expérience (XDM) associé au jeu de données. |
| `identities` | Un tableau contenant les identités d’au moins un utilisateur dont vous souhaitez supprimer les informations. Chaque identité se compose d’une [namespace d’identité](../../identity-service/namespaces.md) et une valeur :<ul><li>`namespace`: Contient une seule propriété string, `code`, qui représente l’espace de noms de l’identité. </li><li>`id` : la valeur de l’identité.</ul>If `datasetId` spécifie un seul jeu de données, chaque entité sous `identities` doit utiliser le même espace de noms d’identité que l’identité Principale du schéma.<br><br>If `datasetId` est défini sur `ALL`, la variable `identities` n’est limité à aucun espace de noms unique, car chaque jeu de données peut être différent. Toutefois, vos requêtes sont toujours limitées aux espaces de noms disponibles pour votre organisation, comme indiqué par [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

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
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher ultérieurement l’état de la suppression. |
| `orgId` | ID de votre organisation. |
| `batchId` | L’identifiant du lot auquel cette commande de suppression est associée, utilisé à des fins de débogage. Plusieurs commandes de suppression sont regroupées dans un lot qui sera traité par les services en aval. |
| `bundleOrdinal` | L’ordre dans lequel cette commande de suppression a été reçue lorsqu’elle a été regroupée dans un lot pour traitement en aval. Utilisé à des fins de débogage. |
| `payloadByteSize` | Taille, en octets, de la liste des identités fournies dans le payload de requête qui a créé cet ordre de suppression. |
| `operationCount` | Nombre d’identités auxquelles cet ordre de suppression s’applique. |
| `createdAt` | Horodatage de la création de la commande de suppression. |
| `responseMessage` | Dernière réponse renvoyée par le système. Si une erreur se produit lors du traitement, cette valeur est une chaîne JSON contenant des informations détaillées sur les erreurs afin de vous aider à comprendre ce qui s’est passé. |
| `status` | État actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |

{style=&quot;table-layout:auto&quot;}

## Répertorier les états de toutes les suppressions d’identité {#list}

Vous pouvez répertorier les états de toutes les suppressions d’identité en effectuant une requête de GET.

**Format d’API**

```http
GET /workorder?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMS}` | Liste des paramètres de requête facultatifs pour l’appel de liste, avec plusieurs paramètres séparés par `&` caractères. Les paramètres de requête acceptés sont les suivants :<ul><li>`data` - Une valeur booléenne qui, lorsqu’elle est définie sur `true`, inclut toutes les données de requête et de réponse supplémentaires reçues pour l’ordre de suppression. La valeur par défaut est `false`.</li><li>`start` - Horodatage du début de la période pour rechercher les commandes de suppression.</li><li>`end` - Horodatage de la fin de la période pour rechercher les commandes de suppression.</li><li>`page` - Page de réponse spécifique à renvoyer.</li><li>`limit` - Nombre d’enregistrements à afficher par page.</li></ul> |

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

Une réponse réussie renvoie les détails de toutes les opérations de suppression, y compris leur état actuel. La réponse ci-dessous a été réduite pour gagner de l’espace.

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
| `results` | Contient la liste des commandes de suppression et leurs détails. Pour plus d’informations sur les propriétés d’une commande de suppression, voir l’exemple de réponse dans la section sur [recherche d’un ordre de suppression](#lookup). |
| `total` | Nombre total de commandes de suppression trouvées en fonction des filtres actuels. |
| `count` | Nombre total de commandes de suppression trouvées sur chaque page de la réponse. |
| `_links` | Contient des informations de pagination pour vous aider à explorer le reste de la réponse :<ul><li>`next`: Contient une URL pour la page suivante dans la réponse.</li><li>`page`: Contient un modèle d’URL pour accéder à une autre page de la réponse ou ajuster le nombre d’éléments renvoyés sur chaque page.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Récupération de l’état d’une suppression d’identité (#lookup)

Après avoir envoyé une demande à [suppression d’une identité](#delete-identities), vous pouvez vérifier son état à l’aide d’une requête de GET.

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

Une réponse réussie renvoie les détails de l’opération de suppression, y compris son état actuel.

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
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher ultérieurement l’état de la suppression. |
| `orgId` | ID de votre organisation. |
| `batchId` | L’identifiant du lot auquel cette commande de suppression est associée, utilisé à des fins de débogage. Plusieurs commandes de suppression sont regroupées dans un lot qui sera traité par les services en aval. |
| `bundleOrdinal` | L’ordre dans lequel cette commande de suppression a été reçue lorsqu’elle a été regroupée dans un lot pour traitement en aval. Utilisé à des fins de débogage. |
| `payloadByteSize` | Taille, en octets, de la liste des identités fournies dans le payload de requête qui a créé cet ordre de suppression. |
| `operationCount` | Nombre d’identités auxquelles cet ordre de suppression s’applique. |
| `createdAt` | Horodatage de la création de la commande de suppression. |
| `responseMessage` | Dernière réponse renvoyée par le système. Si une erreur se produit lors du traitement, cette valeur est une chaîne JSON contenant des informations détaillées sur les erreurs afin de vous aider à comprendre ce qui s’est passé. |
| `status` | État actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
