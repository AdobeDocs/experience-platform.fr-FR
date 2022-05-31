---
title: Point de terminaison de l’API TTL (Dataset Time-to-Live)
description: Le point d’entrée /ttl de l’API Data Hygiene vous permet de planifier par programmation les TTL du jeu de données dans Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 7%

---

# Point d’entrée TTL (Dataset time-to-live)

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

Le `/ttl` Le point de terminaison de l’API Data Hygiene vous permet de planifier des protocoles TTL (time-to-live) pour les jeux de données dans Adobe Experience Platform.

Un TTL de jeu de données n’est qu’une opération de suppression retardée minutée. Le jeu de données n’est pas protégé dans l’intervalle, il peut donc être supprimé par d’autres moyens avant que son expiration ne soit atteinte.

>[!NOTE]
>
>Bien que l’expiration soit spécifiée comme un instant spécifique dans le temps, un délai pouvant aller jusqu’à 24 heures après l’expiration avant le lancement de la suppression réelle peut être appliqué. Une fois la suppression lancée, il peut s’écouler jusqu’à sept jours avant que toutes les traces du jeu de données aient été supprimées des systèmes Platform.

Avant que la suppression du jeu de données ne soit réellement lancée, vous pouvez annuler la durée de vie (TTL) ou modifier son heure de déclenchement. Après avoir annulé un délai d’expiration, vous pouvez le rouvrir en définissant une nouvelle expiration.

Une fois que la suppression du jeu de données est lancée, son délai d’activation est marqué comme `executing`, et ne peut plus être modifié. Le jeu de données lui-même peut être récupéré pendant sept jours au maximum, mais uniquement par le biais d’un processus manuel initié par le biais d’une demande de service Adobe.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’API Data Hygiene. Avant de poursuivre, veuillez consulter la section [aperçu](./overview.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d’appels API de ce document, ainsi que des informations importantes concernant les en-têtes requis pour réussir les appels à une API Experience Platform.

## Liste des TTL de jeux de données {#list}

Vous pouvez répertorier tous les jeux de données TTL pour votre organisation en effectuant une requête de GET.

**Format d’API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETERS}` | Une liste de paramètres de requête facultatifs, avec plusieurs paramètres séparés par `&` caractères. Les paramètres courants incluent `size` et `page` à des fins de pagination. Pour obtenir la liste complète des paramètres de requête pris en charge, reportez-vous à la section [section de l’annexe](#query-params). |

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

Une réponse réussie liste les TTL obtenus. L’exemple suivant a été tronqué pour l’espace.

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
| `results` | Contient les détails des TTL renvoyés. Pour plus d’informations sur les propriétés d’une entité TTL, consultez la section de réponse pour créer une [appel de recherche](#lookup). |
| `current_page` | Page actuelle des résultats répertoriés. |
| `total_pages` | Nombre total de pages dans la réponse. |
| `total_count` | Nombre total d’entités TTL dans la réponse. |

{style=&quot;table-layout:auto&quot;}

## Recherche d’un TTL {#lookup}

Vous pouvez rechercher un jeu de données TTL par le biais d’une requête de GET.

**Format d’API**

```http
GET /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la durée de vie que vous souhaitez rechercher. |

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

Une réponse réussie renvoie les détails du délai d’activation.

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
| `ttlId` | L’identifiant du jeu de données TTL. |
| `datasetId` | L’identifiant du jeu de données auquel ce délai d’activation s’applique. |
| `imsOrg` | ID de votre organisation. |
| `status` | État actuel du délai d’activation. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de la durée de vie. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour le délai d’activation. |

{style=&quot;table-layout:auto&quot;}

## Création d’un TTL {#create}

Vous pouvez ajouter un TTL pour un jeu de données par le biais d’une requête de POST.

**Format d’API**

```http
POST /ttl
```

**Requête**

La requête suivante planifie un jeu de données. `5b020a27e7040801dedbf46e` pour suppression à la fin de 2022 (heure de Greenwich).

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
| `datasetId` | L’identifiant du jeu de données pour lequel vous souhaitez planifier un TTL. |
| `expiry` | Horodatage ISO 8601 indiquant le moment où le jeu de données sera supprimé. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de la durée de vie, avec l’état HTTP 200 (OK) si une durée de vie préexistante a été mise à jour, ou 201 (Created) s’il n’y avait pas de durée de vie préexistante.

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
| `ttlId` | L’identifiant du jeu de données TTL. |
| `datasetId` | L’identifiant du jeu de données auquel ce délai d’activation s’applique. |
| `imsOrg` | ID de votre organisation. |
| `status` | État actuel du délai d’activation. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de la durée de vie. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour le délai d’activation. |

{style=&quot;table-layout:auto&quot;}

## Mise à jour d’un TTL {#update}

Vous pouvez mettre à jour un TTL pour un jeu de données par le biais d’une requête de PUT.

**Format d’API**

```http
PUT /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la durée de vie que vous souhaitez modifier. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour le délai d’activation du jeu de données. `5b020a27e7040801dedbf46e` il expire donc fin 2023 (l&#39;heure de Greenwich).

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
| `expiry` | Horodatage ISO 8601 indiquant le moment où le jeu de données sera supprimé. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails de la durée de vie mise à jour.

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
| `ttlId` | L’identifiant du jeu de données TTL. |
| `datasetId` | L’identifiant du jeu de données auquel ce délai d’activation s’applique. |
| `imsOrg` | ID de votre organisation. |
| `status` | État actuel du délai d’activation. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de la durée de vie. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour le délai d’activation. |

{style=&quot;table-layout:auto&quot;}

## Annulation d’un TTL {#delete}

Vous pouvez annuler une durée de vie (TTL) en effectuant une requête de DELETE.

**Format d’API**

```http
DELETE /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la durée de vie que vous souhaitez annuler. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante met à jour le délai d’activation du jeu de données. `5b020a27e7040801dedbf46e` il expire donc fin 2023 (l&#39;heure de Greenwich).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la durée de vie, avec son `status` est maintenant défini sur `cancelled`.

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
| `ttlId` | L’identifiant du jeu de données TTL. |
| `datasetId` | L’identifiant du jeu de données auquel ce délai d’activation s’applique. |
| `imsOrg` | ID de votre organisation. |
| `status` | État actuel du délai d’activation. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Horodatage de la dernière mise à jour de la durée de vie. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour le délai d’activation. |

{style=&quot;table-layout:auto&quot;}

## Récupération de l’historique d’un TTL

Vous pouvez rechercher l’historique d’un TTL spécifique à l’aide du paramètre de requête . `include=history` dans une requête de recherche. Le résultat comprend des informations sur la création de la durée de vie (TTL), les mises à jour qui ont été appliquées et son annulation ou son exécution (le cas échéant).

**Format d’API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Paramètre | Description |
| --- | --- |
| `{TTL_ID}` | L’identifiant de la durée de vie dont vous souhaitez consulter l’historique. |

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

Une réponse réussie renvoie les détails du délai d’activation, avec une `history` tableau fournissant les détails `status`, `expiry`, `updatedAt`, et `updatedBy` attributs pour chacune de ses mises à jour enregistrées.

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
| `ttlId` | L’identifiant du jeu de données TTL. |
| `datasetId` | L’identifiant du jeu de données auquel ce délai d’activation s’applique. |
| `imsOrg` | ID de votre organisation. |
| `history` | Répertorie l’historique des mises à jour pour le TTL sous la forme d’un tableau d’objets, chaque objet contenant le `status`, `expiry`, `updatedAt`, et `updatedBy` attributs pour le délai d’activation au moment de la mise à jour. |

{style=&quot;table-layout:auto&quot;}

## Annexe

### Paramètres de requête acceptés {#query-params}

Le tableau suivant décrit les paramètres de requête disponibles lors de la [liste des TTL des jeux de données](#list):

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `size` | Entier compris entre 1 et 100 qui indique le nombre maximal de TTL à renvoyer. La valeur par défaut est 25. | `size=50` |
| `page` | Entier qui indique la page de TTL à renvoyer. | `page=3` |
| `status` | Liste d’états séparés par des virgules. Lorsqu’elle est incluse, la réponse correspond aux TTL dont l’état actuel fait partie de ceux répertoriés. | `status=pending,cancelled` |
| `author` | Correspond aux TTL dont les `created_by` correspond à la chaîne de recherche. Si la chaîne de recherche commence par `LIKE` ou `NOT LIKE`, le reste est traité comme un modèle de recherche SQL. Dans le cas contraire, l’intégralité de la chaîne de recherche est traitée comme une chaîne littérale qui doit correspondre exactement à l’intégralité du contenu d’une `created_by` champ . | `author=LIKE %john%` |
| `createdDate` | Correspond aux TTL qui ont été créés dans la fenêtre de 24 heures à partir de l’heure indiquée.<br><br>Notez que les dates sans heure (comme `2021-12-07`) représente la date et l’heure au début de cette journée. Ainsi, `createdDate=2021-12-07` fait référence à tout TTL créé le 7 décembre 2021 à partir de `00:00:00` through `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Correspond aux TTL qui ont été créés à l’heure indiquée ou après cette date. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Correspond aux TTL qui ont été créés à l’heure indiquée ou avant. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Comme `createdDate` / `createdFromDate` / `createdToDate`, mais correspond à l’heure de mise à jour d’un TTL plutôt qu’à l’heure de création.<br><br>Une durée de vie (TTL) est considérée comme mise à jour à chaque modification, y compris lorsqu’elle est créée, annulée ou exécutée. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Correspond aux TTL qui ont été annulés à tout moment dans l’intervalle indiqué. Cela s’applique même si la durée de vie a été rouverte ultérieurement (en définissant une nouvelle expiration pour le même jeu de données). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Correspond aux TTL qui ont été effectués au cours de l’intervalle spécifié. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Correspond aux TTL qui doivent être exécutés, ou qui ont déjà été exécutés, au cours de l’intervalle spécifié. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
