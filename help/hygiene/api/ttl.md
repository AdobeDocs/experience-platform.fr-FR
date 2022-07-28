---
title: Point d’entrée de l’API Dataset Time-to-Live (TTL)
description: Le point d’entrée /ttl de l’API Data Hygiene vous permet de planifier par programmation les TTL de jeux de données dans Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 98%

---

# Point d’entrée de durée de vie (TTL) de jeu de données

>[!IMPORTANT]
>
>Actuellement, seules les organisations qui ont acheté Healthcare Shield disposent des capacités d’hygiène des données dans Adobe Experience Platform.

Le point d’entrée `/ttl` de l’API Data Hygiene vous permet de planifier des protocoles de durée de vie (TTL) pour les jeux de données dans Adobe Experience Platform.

Une TTL de jeu de données n’est qu’une opération de suppression différée. En attendant, le jeu de données n’est pas protégé, il peut donc être supprimé par d’autres moyens avant son expiration.

>[!NOTE]
>
>Bien que l’expiration soit spécifiée comme un instant spécifique dans le temps, la suppression effective peut prendre jusqu’à 24 heures après l’expiration. Une fois la suppression lancée, il peut s’écouler jusqu’à sept jours avant que toutes les traces du jeu de données aient été supprimées des systèmes Platform.

Avant que la suppression du jeu de données ne soit réellement lancée, vous pouvez annuler la TTL ou modifier son heure de déclenchement. Après l’annulation d’une TTL, vous pouvez la rouvrir en définissant une nouvelle expiration.

Une fois que la suppression du jeu de données est lancée, sa TTL est marquée comme étant `executing` et ne peut plus être modifiée. Le jeu de données lui-même peut être récupéré pendant un maximum de sept jours, mais uniquement par le biais d’un processus manuel initié par une demande de service Adobe.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de continuer, consultez la [présentation](./overview.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Répertorier des TTL de jeux de données {#list}

Vous pouvez répertorier toutes les TTL de jeux de données pour votre organisation en effectuant une requête GET.

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

Une réponse réussie répertorie les TTL obtenues. L’exemple suivant a été tronqué pour des raisons d’espace.

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
| `results` | Contient les détails des TTL renvoyées. Pour plus d’informations sur les propriétés d’une entité de TTL, consultez la section de réponse pour effectuer un [appel de recherche](#lookup). |
| `current_page` | Page actuelle des résultats répertoriés. |
| `total_pages` | Nombre total de pages dans la réponse. |
| `total_count` | Nombre total d’entités de TTL dans la réponse. |

{style=&quot;table-layout:auto&quot;}

## Rechercher une TTL {#lookup}

Vous pouvez rechercher une TTL de jeu de données par le biais d’une requête GET.

**Format d’API**

```http
GET /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la TTL que vous souhaitez rechercher. |

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

Une réponse réussie renvoie les détails de la TTL.

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
| `ttlId` | L’identifiant de la TTL de jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette TTL s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | Statut actuel de la TTL. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Date et heure de la dernière mise à jour de la TTL. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour la TTL. |

{style=&quot;table-layout:auto&quot;}

## Créer une TTL {#create}

Vous pouvez ajouter une TTL à un jeu de données par le biais d’une requête POST.

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
| `datasetId` | L’identifiant du jeu de données pour lequel vous souhaitez planifier une TTL. |
| `expiry` | Date et heure ISO 8601 indiquant le moment de la suppression du jeu de données. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de la TTL, avec le statut HTTP 200 (OK) si une TTL préexistante a été mise à jour ou 201 (Created) en l’absence de TTL préexistante.

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
| `ttlId` | L’identifiant de la TTL de jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette TTL s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | Statut actuel de la TTL. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Date et heure de la dernière mise à jour de la TTL. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour la TTL. |

{style=&quot;table-layout:auto&quot;}

## Mettre à jour une TTL {#update}

Vous pouvez mettre à jour une TTL pour un jeu de données par le biais d’une requête PUT.

**Format d’API**

```http
PUT /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la TTL que vous souhaitez modifier. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour la TTL du jeu de données `5b020a27e7040801dedbf46e` pour qu’il expire à la fin de 2023 (heure de Greenwich).

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

Une réponse réussie renvoie les détails de la TTL mise à jour.

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
| `ttlId` | L’identifiant de la TTL de jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette TTL s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | Statut actuel de la TTL. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Date et heure de la dernière mise à jour de la TTL. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour la TTL. |

{style=&quot;table-layout:auto&quot;}

## Annuler une TTL {#delete}

Vous pouvez annuler une TTL en effectuant une requête DELETE.

**Format d’API**

```http
DELETE /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la TTL que vous souhaitez annuler. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour la TTL du jeu de données `5b020a27e7040801dedbf46e` pour qu’il expire à la fin de 2023 (heure de Greenwich).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la TTL, avec l’attribut `status` désormais défini sur `cancelled`.

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
| `ttlId` | L’identifiant de la TTL de jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette TTL s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `status` | Statut actuel de la TTL. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Date et heure de la dernière mise à jour de la TTL. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour la TTL. |

{style=&quot;table-layout:auto&quot;}

## Récupérer l’historique d’une TTL

Vous pouvez rechercher l’historique d’une TTL spécifique à l’aide du paramètre de requête `include=history` dans une requête de recherche. Le résultat comprend des informations sur la création de la TTL, les mises à jour qui ont été appliquées et son annulation ou son exécution (le cas échéant).

**Format d’API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la TTL dont vous souhaitez rechercher l’historique. |

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

Une réponse réussie renvoie les détails de la TTL, avec un tableau `history` fournissant les détails des attributs `status`, `expiry`, `updatedAt` et `updatedBy` pour chacune des mises à jour enregistrées.

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
| `ttlId` | L’identifiant de la TTL de jeu de données. |
| `datasetId` | L’identifiant du jeu de données auquel cette TTL s’applique. |
| `imsOrg` | L’identifiant de l’organisation. |
| `history` | Répertorie l’historique des mises à jour pour la TTL sous la forme d’un tableau d’objets, chaque objet contenant les attributs `status`, `expiry`, `updatedAt` et `updatedBy` de la TTL au moment de la mise à jour. |

{style=&quot;table-layout:auto&quot;}

## Annexe

### Paramètres de requête acceptés {#query-params}

Le tableau suivant décrit les paramètres de requête disponibles lorsque les [TTL des jeux de données sont répertoriés](#list) :

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `size` | Nombre entier compris entre 1 et 100 qui indique le nombre maximal de TTL à renvoyer. La valeur par défaut est 25. | `size=50` |
| `page` | Nombre entier qui indique la page des TTL à renvoyer. | `page=3` |
| `status` | Liste de statuts séparés par des virgules. Lorsqu’elle est incluse, la réponse correspond aux TTL dont le statut actuel fait partie de celles répertoriées. | `status=pending,cancelled` |
| `author` | Correspond aux TTL dont `created_by` correspond à la chaîne de recherche. Si la chaîne de recherche commence par `LIKE` ou `NOT LIKE`, le reste est traité comme un modèle de recherche SQL. Dans le cas contraire, l’intégralité de la chaîne de recherche est traitée comme une chaîne littérale qui doit correspondre exactement à l’intégralité du contenu d’un champ `created_by`. | `author=LIKE %john%` |
| `createdDate` | Correspond aux TTL qui ont été créées dans la fenêtre de 24 heures à partir de l’heure indiquée.<br><br>Notez que les dates sans heure (comme `2021-12-07`) représentent la date/heure au début de la journée. Ainsi, `createdDate=2021-12-07` fait référence à l’ensemble des TTL créées le 7 décembre 2021, de `00:00:00` à `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Correspond aux TTL qui ont été créées à l’heure indiquée ou ultérieurement. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Correspond aux TTL qui ont été créées à l’heure indiquée ou antérieurement. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Comme `createdDate` / `createdFromDate` / `createdToDate`, mais correspond à l’heure de mise à jour d’une TTL plutôt qu’à l’heure de création.<br><br>Une TTL est considérée comme mise à jour à chaque modification, y compris lorsqu’elle est créée, annulée ou exécutée. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Correspond aux TTL qui ont été annulées à tout moment dans l’intervalle indiqué. Cela s’applique même si la TTL a été rouverte ultérieurement (en définissant une nouvelle expiration pour le même jeu de données). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Correspond aux TTL qui ont été effectuées au cours de l’intervalle spécifié. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Correspond aux TTL qui doivent être exécutées, ou qui ont déjà été exécutées, au cours de l’intervalle spécifié. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
