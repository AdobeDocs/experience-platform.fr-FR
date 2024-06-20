---
title: Point de terminaison de l’API Work Order
description: Le point d’entrée /workorder de l’API Data Hygiene vous permet de gérer par programmation les tâches de suppression pour les identités.
badgeBeta: label="Version bêta" type="Informative"
role: Developer
badge: Version bêta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: bf819d506b0ee6f3aba6850f598ee46f16695dfa
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 56%

---

# Point d’entrée de l’ordre de travail {#work-order-endpoint}

La variable `/workorder` Le point de terminaison de l’API Data Hygiene vous permet de gérer par programmation les demandes de suppression d’enregistrements dans Adobe Experience Platform.

>[!IMPORTANT]
> 
>La fonction de suppression d’enregistrement est actuellement en version bêta et disponible uniquement dans un **version limitée**. Il n’est pas disponible pour tous les clients. Les demandes de suppression d’enregistrements ne sont disponibles que pour les organisations de la version limitée.
>
>Les suppressions d’enregistrements sont destinées au nettoyage des données, à la suppression des données anonymes ou à la minimisation des données. Elles ne sont **pas** destinées aux demandes de droits des titulaires de données (conformité) en ce qui concerne les réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD). Pour tous les cas d’utilisation de conformité, utilisez plutôt [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de continuer, consultez la [présentation](./overview.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Création d’une requête de suppression d’enregistrement {#create}

Vous pouvez supprimer une ou plusieurs identités d’un seul jeu de données ou de tous les jeux de données en adressant une requête POST à la variable `/workorder` point de terminaison .

>[!IMPORTANT]
> 
>Il existe différentes limites pour le nombre total de suppressions d’enregistrement d’identité unique qui peuvent être envoyées chaque mois. Ces limites sont basées sur votre contrat de licence. Les organisations qui ont acheté toutes les éditions d’Adobe Real-time Customer Data Platform et de Adobe Journey Optimizer peuvent envoyer jusqu’à 100 000 enregistrements d’identité supprimés chaque mois. Organisations ayant effectué des achats **Adobe Health Care Shield** ou **Adobe de la confidentialité et de la sécurité** peut envoyer jusqu’à 600 000 enregistrements d’identité supprimés chaque mois.<br>Une seule [demande de suppression d’enregistrement via l’interface utilisateur](../ui/record-delete.md) vous permet d’envoyer 10 000 identifiants à la fois. La méthode d’API pour supprimer des enregistrements permet l’envoi simultané de 100 000 identifiants.<br>Il est recommandé d’envoyer autant d’ID par demande que possible, jusqu’à votre limite d’ID. Lorsque vous envisagez de supprimer un volume élevé d’identifiants, il est préférable d’éviter d’envoyer un volume faible ou une seule demande de suppression d’identifiant par enregistrement.

**Format d’API**

```http
POST /workorder
```

>[!NOTE]
>
>Les requêtes de cycle de vie des données peuvent uniquement modifier des jeux de données en fonction d’identités principales ou d’une carte d’identité. Une requête doit spécifier l’identité principale ou fournir une carte d’identité.

**Requête**

Selon la valeur de la variable `datasetId` fourni dans le payload de requête, l’appel API supprime les identités de tous les jeux de données ou d’un seul jeu de données que vous spécifiez. La requête suivante supprime trois identités d’un jeu de données spécifique.

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
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
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
| `action` | L’action à effectuer. La valeur doit être définie sur `delete_identity` pour les suppressions d’enregistrement. |
| `datasetId` | Si vous effectuez une suppression dans un seul jeu de données, cette valeur doit correspondre à l’identifiant du jeu de données en question. Si vous effectuez une suppression dans tous les jeux de données, définissez la valeur sur `ALL`.<br><br>Si vous spécifiez un seul jeu de données, une identité principale doit être définie pour le schéma XDM (Experience Data Model) associé au jeu de données. Si le jeu de données ne possède pas d’identité principale, il doit alors disposer d’une carte d’identité pour pouvoir être modifié par une requête Data Lifecycle.<br>Si une carte d’identité existe, elle est présente sous la forme d’un champ de niveau supérieur nommé `identityMap`.<br>Notez qu’une ligne de jeu de données peut avoir de nombreuses identités dans sa carte d’identité, mais qu’une seule peut être marquée comme principale. `"primary": true` doit être inclus pour forcer la variable `id` pour correspondre à une identité principale. |
| `displayName` | Nom d’affichage de la requête de suppression d’enregistrement. |
| `description` | Description de la requête de suppression d’enregistrement. |
| `identities` | Un tableau contenant les identités d’au moins un utilisateur dont vous souhaitez supprimer les informations. Chaque identité se compose d’un [espace de noms d’identité](../../identity-service/features/namespaces.md) et d’une valeur :<ul><li>`namespace` : contient une seule propriété de chaîne, `code`, qui représente l’espace de noms d’identité. </li><li>`id` : la valeur de l’identité.</ul>Si `datasetId` spécifie un seul jeu de données, chaque entité sous `identities` doit utiliser le même espace de noms d’identité que l’identité principale du schéma.<br><br>Si `datasetId` est défini sur `ALL`, le tableau `identities` n’est limité à aucun espace de noms unique, car chaque jeu de données peut être différent. Toutefois, les requêtes sont toujours limitées aux espaces de noms disponibles pour l’organisation, comme indiqué par le [service d’identités](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la suppression de l’enregistrement.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | Votre identifiant d’organisation. |
| `bundleId` | L’identifiant de l’offre groupée à laquelle cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés pour être traités par les services en aval. |
| `action` | L’action effectuée par l’ordre de travail. Pour les suppressions d’enregistrement, la valeur est `identity-delete`. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `updatedAt` | La date et l’heure de la dernière mise à jour de l’ordre de suppression. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
| `datasetId` | L’identifiant du jeu de données sujet à la requête. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |

{style="table-layout:auto"}

## Récupération de l’état d’une suppression d’enregistrement {#lookup}

Après vous [créer une requête de suppression d’enregistrement](#create), vous pouvez vérifier son état à l’aide d’une requête de GET.

**Format d’API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | La variable `workorderId` de l’enregistrement que vous recherchez. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’opération de suppression, y compris son statut actuel.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | Votre identifiant d’organisation. |
| `bundleId` | L’identifiant de l’offre groupée à laquelle cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés pour être traités par les services en aval. |
| `action` | L’action effectuée par l’ordre de travail. Pour les suppressions d’enregistrement, la valeur est `identity-delete`. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `updatedAt` | La date et l’heure de la dernière mise à jour de l’ordre de suppression. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
| `datasetId` | L’identifiant du jeu de données sujet à la requête. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |
| `productStatusDetails` | Un tableau qui répertorie le statut actuel des processus en aval liés à la requête. Chaque objet Tableau contient les propriétés suivantes :<ul><li>`productName` : le nom du service en aval.</li><li>`productStatus` : le statut actuel du traitement de la requête du service en aval.</li><li>`createdAt` : la date et l’heure auxquelles le statut le plus récent a été publié par le service.</li></ul> |

## Mise à jour d’une requête de suppression d’enregistrement

Vous pouvez mettre à jour la variable `displayName` et `description` pour une suppression d’enregistrement en effectuant une requête de PUT.

**Format d’API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | La variable `workorderId` de l’enregistrement que vous recherchez. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Propriété | Description |
| --- | --- |
| `displayName` | Nom d’affichage mis à jour pour la requête de suppression d’enregistrement. |
| `description` | Description mise à jour de la requête de suppression d’enregistrement. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la suppression de l’enregistrement.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `workorderId` | L’identifiant de l’ordre de suppression. Vous pouvez l’utiliser pour rechercher le statut de la suppression ultérieurement. |
| `orgId` | Votre identifiant d’organisation. |
| `bundleId` | L’identifiant de l’offre groupée à laquelle cet ordre de suppression est associé, utilisé à des fins de débogage. Plusieurs ordres de suppression sont regroupés pour être traités par les services en aval. |
| `action` | L’action effectuée par l’ordre de travail. Pour les suppressions d’enregistrement, la valeur est `identity-delete`. |
| `createdAt` | La date et l’heure de création de l’ordre de suppression. |
| `updatedAt` | La date et l’heure de la dernière mise à jour de l’ordre de suppression. |
| `status` | Le statut actuel de l’ordre de suppression. |
| `createdBy` | L’utilisateur qui a créé l’ordre de suppression. |
| `datasetId` | L’identifiant du jeu de données sujet à la requête. Si la requête porte sur tous les jeux de données, la valeur est définie sur `ALL`. |
| `productStatusDetails` | Un tableau qui répertorie le statut actuel des processus en aval liés à la requête. Chaque objet Tableau contient les propriétés suivantes :<ul><li>`productName` : le nom du service en aval.</li><li>`productStatus` : le statut actuel du traitement de la requête du service en aval.</li><li>`createdAt` : la date et l’heure auxquelles le statut le plus récent a été publié par le service.</li></ul> |

{style="table-layout:auto"}
