---
title: Point de terminaison de l’API d’expiration des jeux de données
description: Le point d’entrée /ttl de l’API Data Hygiene vous permet de planifier par programmation l’expiration des jeux de données dans Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 49ba5263c6dc8eccac2ffe339476cf316c68e486
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 34%

---

# Point d’entrée d’expiration du jeu de données

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités de nettoyage de données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté Healthcare Shield.

Le `/ttl` Le point de terminaison de l’API Data Hygiene vous permet de planifier des dates d’expiration pour les jeux de données dans Adobe Experience Platform.

L’expiration d’un jeu de données n’est qu’une opération de suppression retardée et minutée. En attendant, le jeu de données n’est pas protégé, il peut donc être supprimé par d’autres moyens avant son expiration.

>[!NOTE]
>
>Bien que l’expiration soit spécifiée comme un instant spécifique dans le temps, la suppression effective peut prendre jusqu’à 24 heures après l’expiration. Une fois la suppression lancée, il peut s’écouler jusqu’à sept jours avant que toutes les traces du jeu de données aient été supprimées des systèmes Platform.

À tout moment avant que la suppression du jeu de données ne soit réellement lancée, vous pouvez annuler l’expiration ou modifier son heure de déclenchement. Après avoir annulé l’expiration d’un jeu de données, vous pouvez le rouvrir en définissant une nouvelle expiration.

Une fois que la suppression du jeu de données est lancée, sa tâche d’expiration est marquée comme `executing`, et ne peut plus être modifié. Le jeu de données lui-même peut être récupéré pendant un maximum de sept jours, mais uniquement par le biais d’un processus manuel initié par une demande de service Adobe. Lorsque la requête s’exécute, le lac de données, Identity Service et Real-time Customer Profile commencent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Une fois les données supprimées des trois services, l’expiration est marquée comme `executed`.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de continuer, consultez la [présentation](./overview.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Liste des expirations de jeux de données {#list}

Vous pouvez répertorier toutes les expirations de jeux de données pour votre organisation en effectuant une requête de GET.

**Format d’API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETERS}` | Une liste de paramètres de requête facultatifs avec plusieurs paramètres séparés par des caractères `&`. Les paramètres courants comprennent `size` et `page` à des fins de pagination. Pour obtenir la liste complète des paramètres de requête pris en charge, consultez la [section Annexe](#query-params). |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie liste les expirations de jeux de données résultantes. L’exemple suivant a été tronqué pour des raisons d’espace.

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| Propriété | Description |
| --- | --- |
| `results` | Contient les détails des expirations de jeu de données renvoyées. Pour plus d’informations sur les propriétés d’expiration d’un jeu de données, reportez-vous à la section de réponse pour effectuer une [appel de recherche](#lookup). |
| `current_page` | Page actuelle des résultats répertoriés. |
| `total_pages` | Nombre total de pages dans la réponse. |
| `total_count` | Nombre total d’expirations de jeux de données dans la réponse. |

{style=&quot;table-layout:auto&quot;}

## Recherche d’une expiration de jeu de données {#lookup}

Vous pouvez rechercher une expiration de jeu de données par le biais d’une requête de GET.

**Format d’API**

```http
GET /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de l’expiration du jeu de données que vous souhaitez rechercher. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | L’identifiant de l’expiration du jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette expiration s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | État actuel de l’expiration du jeu de données. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de l’expiration. |
| `updatedBy` | L’utilisateur qui a mis à jour la dernière expiration. |

{style=&quot;table-layout:auto&quot;}

## Création d’une expiration de jeu de données {#create}

Vous pouvez créer une date d’expiration pour un jeu de données par le biais d’une requête de POST.

**Format d’API**

```http
POST /ttl
```

**Requête**

La requête suivante planifie la suppression d’un jeu de données `5b020a27e7040801dedbf46e` à la fin de 2022 (heure de Greenwich).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| Propriété | Description |
| --- | --- |
| `datasetId` | L’identifiant du jeu de données pour lequel vous souhaitez planifier une date d’expiration. |
| `expiry` | Date et heure ISO 8601 indiquant le moment de la suppression du jeu de données. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données, avec l’état HTTP 200 (OK) si une expiration préexistante a été mise à jour, ou 201 (Created) si aucune expiration préexistante n’a été mise à jour.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | L’identifiant de l’expiration du jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette expiration s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | État actuel de l’expiration du jeu de données. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de l’expiration. |
| `updatedBy` | L’utilisateur qui a mis à jour la dernière expiration. |

{style=&quot;table-layout:auto&quot;}

## Mettre à jour l’expiration d’un jeu de données {#update}

Vous pouvez mettre à jour l’expiration d’un jeu de données par le biais d’une requête de PUT.

**Format d’API**

```http
PUT /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de l’expiration du jeu de données que vous souhaitez modifier. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour l’expiration du jeu de données. `5b020a27e7040801dedbf46e` il expire donc fin 2023 (l&#39;heure de Greenwich).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| Propriété | Description |
| --- | --- |
| `expiry` | Date et heure ISO 8601 indiquant le moment de la suppression du jeu de données. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de l’expiration mise à jour.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | L’identifiant de l’expiration du jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette expiration s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | État actuel de l’expiration du jeu de données. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de l’expiration. |
| `updatedBy` | L’utilisateur qui a mis à jour la dernière expiration. |

{style=&quot;table-layout:auto&quot;}

## Annulation de l’expiration d’un jeu de données {#delete}

Vous pouvez annuler l’expiration d’un jeu de données en effectuant une requête de DELETE.

**Format d’API**

```http
DELETE /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de l’expiration du jeu de données que vous souhaitez annuler. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour l’expiration du jeu de données. `5b020a27e7040801dedbf46e` il expire donc fin 2023 (l&#39;heure de Greenwich).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données, avec son `status` est maintenant défini sur `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | L’identifiant de l’expiration du jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette expiration s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | État actuel de l’expiration du jeu de données. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de l’expiration. |
| `updatedBy` | L’utilisateur qui a mis à jour la dernière expiration. |

{style=&quot;table-layout:auto&quot;}

## Récupération de l’historique de l’expiration d’un jeu de données

Vous pouvez rechercher l’historique d’une expiration de jeu de données spécifique à l’aide du paramètre de requête . `include=history` dans une requête de recherche. Le résultat comprend des informations sur la création de l’expiration du jeu de données, les mises à jour qui ont été appliquées et son annulation ou son exécution (le cas échéant).

**Format d’API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de l’expiration du jeu de données dont vous souhaitez rechercher l’historique. |

{style=&quot;table-layout:auto&quot;}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données, avec une `history` tableau fournissant les détails `status`, `expiry`, `updatedAt`, et `updatedBy` attributs pour chacune de ses mises à jour enregistrées.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | L’identifiant de l’expiration du jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette expiration s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `history` | Répertorie l’historique des mises à jour pour l’expiration sous la forme d’un tableau d’objets, chaque objet contenant la variable `status`, `expiry`, `updatedAt`, et `updatedBy` attributs pour l’expiration au moment de la mise à jour. |

{style=&quot;table-layout:auto&quot;}

## Annexe

### Paramètres de requête acceptés {#query-params}

Le tableau suivant décrit les paramètres de requête disponibles lors de la [liste des expirations de jeux de données](#list):

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `size` | Entier compris entre 1 et 100 indiquant le nombre maximal d’expirations à renvoyer. La valeur par défaut est 25. | `size=50` |
| `page` | Entier qui indique la page d’expiration à renvoyer. | `page=3` |
| `status` | Liste de statuts séparés par des virgules. Lorsqu’elle est incluse, la réponse correspond aux expirations de jeux de données dont l’état actuel fait partie de ceux répertoriés. | `status=pending,cancelled` |
| `author` | Correspond aux expirations dont `created_by` correspond à la chaîne de recherche. Si la chaîne de recherche commence par `LIKE` ou `NOT LIKE`, le reste est traité comme un modèle de recherche SQL. Dans le cas contraire, l’intégralité de la chaîne de recherche est traitée comme une chaîne littérale qui doit correspondre exactement à l’intégralité du contenu d’un champ `created_by`. | `author=LIKE %john%` |
| `createdDate` | Correspond aux expirations créées dans la fenêtre de 24 heures à partir de l’heure indiquée.<br><br>Notez que les dates sans heure (comme `2021-12-07`) représentent la date/heure au début de la journée. Ainsi, `createdDate=2021-12-07` fait référence à toute expiration créée le 7 décembre 2021, à partir de `00:00:00` through `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Correspond aux expirations qui ont été créées à l’heure indiquée ou après cette date. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Correspond aux expirations qui ont été créées à l’heure indiquée ou avant. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Comme `createdDate` / `createdFromDate` / `createdToDate`, mais correspond à l’heure de mise à jour d’un jeu de données au lieu de l’heure de création.<br><br>Une expiration est considérée comme mise à jour à chaque modification, y compris lorsqu’elle est créée, annulée ou exécutée. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Correspond aux expirations qui ont été annulées à tout moment dans l’intervalle indiqué. Cela s’applique même si l’expiration a été rouverte ultérieurement (en définissant une nouvelle expiration pour le même jeu de données). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Correspond aux expirations qui ont été effectuées pendant l’intervalle spécifié. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Correspond aux expirations qui doivent être exécutées, ou qui ont déjà été exécutées, dans l’intervalle spécifié. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
