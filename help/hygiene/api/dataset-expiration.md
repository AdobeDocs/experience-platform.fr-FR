---
title: Point d’entrée de l’API d’expiration du jeu de données
description: Le point d’entrée /ttl de l’API Data Hygiene vous permet de planifier par programmation l’expiration des jeux de données dans Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: a954059155857e6dde7884cf413561cd5214d9bb
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 78%

---

# Point d’entrée d’expiration du jeu de données

Le point d’entrée `/ttl` de l’API Data Hygiene vous permet de planifier des dates d’expiration pour les jeux de données dans Adobe Experience Platform.

L’expiration d’un jeu de données n’est rien d’autre qu’une opération de suppression différée. En attendant, le jeu de données n’est pas protégé, il peut donc être supprimé par d’autres moyens avant son expiration.

>[!NOTE]
>
>Bien que l’expiration soit spécifiée comme un instant spécifique dans le temps, la suppression effective peut prendre jusqu’à 24 heures après l’expiration. Une fois la suppression lancée, il peut s’écouler jusqu’à sept jours avant que toutes les traces du jeu de données aient été supprimées des systèmes Platform.

Avant que la suppression du jeu de données ne soit réellement lancée, vous pouvez annuler l’expiration ou modifier son heure de déclenchement. Après l’annulation de l’expiration d’un jeu de données, vous pouvez la rouvrir en définissant une nouvelle expiration.

Une fois que la suppression du jeu de données est lancée, sa tâche d’expiration est marquée comme étant `executing` et ne peut plus être modifiée. Le jeu de données lui-même peut être récupéré pendant un maximum de sept jours, mais uniquement par le biais d’un processus manuel initié par une demande de service Adobe. Lorsque la requête s’exécute, le lac de données, Identity Service et Real-Time Customer Profile commencent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Une fois les données supprimées des trois services, la tâche d’expiration est marquée comme étant `executed`.

>[!WARNING]
>
>Si un jeu de données est défini pour expirer, vous devez modifier manuellement les flux de données susceptibles d’ingérer des données dans ce jeu, afin que vos workflows en aval ne soient pas affectés négativement.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, veuillez consulter la section [Guide de l’API](./overview.md) pour plus d’informations sur les en-têtes requis pour les opérations CRUD, les messages d’erreur, les collections Postman et la lecture d’exemples d’appels API.

>[!IMPORTANT]
>
>Lorsque vous effectuez des appels vers l’API d’hygiène des données, vous devez utiliser le paramètre -H `x-sandbox-name: {SANDBOX_NAME}` en-tête .

## Répertorier les expirations des jeux de données {#list}

Vous pouvez répertorier toutes les expirations de jeux de données pour votre organisation en effectuant une requête GET. Les paramètres de requête peuvent être utilisés pour filtrer la réponse pour obtenir les résultats appropriés.

**Format d’API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETERS}` | Une liste de paramètres de requête facultatifs avec plusieurs paramètres séparés par des caractères `&`. Les paramètres courants comprennent `limit` et `page` à des fins de pagination. Pour obtenir la liste complète des paramètres de requête pris en charge, consultez la [section Annexe](#query-params). |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie répertorie les expirations de jeux de données obtenues. L’exemple suivant a été tronqué pour des raisons d’espace.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Propriété | Description |
| --- | --- |
| `totalRecords` | Le nombre d’expirations de jeux de données qui correspondaient aux paramètres de l’appel de liste. |
| `ttlDetails` | Contient les détails des expirations de jeux de données renvoyées. Pour plus d’informations sur les propriétés d’une expiration de jeu de données, consultez la section de réponse pour effectuer un [appel de recherche](#lookup). |

{style="table-layout:auto"}

## Rechercher l’expiration d’un jeu de données {#lookup}

Pour rechercher une expiration de jeu de données, effectuez une requête GET avec l’une des options suivantes : `datasetId` ou le `ttlId`.

**Format d’API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | L’identifiant du jeu de données dont vous souhaitez rechercher l’expiration. |
| `{TTL_ID}` | Identifiant de l’expiration du jeu de données. |

{style="table-layout:auto"}

**Requête**

La requête suivante recherche les détails d’expiration du jeu de données `62759f2ede9e601b63a2ee14` :

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données.

<!-- Is there a different response from making a GET request to either '/ttl/{DATASET_ID}?include=history' or '/ttl/{TTL_ID}'? If so please can you provide the response for both (or just the ttl endpoint itf it differs from teh example) -->

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | Identifiant de l’expiration du jeu de données. |
| `datasetId` | Identifiant du jeu de données auquel cette expiration s’applique. |
| `datasetName` | Le nom d’affichage du jeu de données auquel cette expiration s’applique. |
| `sandboxName` | Le nom du sandbox sous lequel se trouve le jeu de données cible. |
| `imsOrg` | Identifiant de l’organisation. |
| `status` | Statut actuel de l’expiration du jeu de données. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Date et heure de la dernière mise à jour de l’expiration. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour l’expiration. |
| `displayName` | Le nom d’affichage de la requête d’expiration. |
| `description` | Une description de la requête d’expiration. |

{style="table-layout:auto"}

### Balises d’expiration du catalogue

Lors de l’utilisation de l’[API Catalog](../../catalog/api/getting-started.md) pour rechercher les détails du jeu de données, si le jeu de données a une expiration active, il sera répertorié sous `tags.adobe/hygiene/ttl`.

Le fichier JSON suivant représente une réponse tronquée pour les détails d’un jeu de données du catalogue, dont la valeur d’expiration est de `32503680000000`. La valeur de la balise code l’expiration comme un nombre entier de millisecondes écoulées depuis le début de l’époque Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Créer ou mettre à jour une expiration de jeu de données {#create-or-update}

Créez ou mettez à jour une date d’expiration pour un jeu de données par le biais d’une requête de PUT. La requête du PUT utilise l’une des méthodes suivantes : `datasetId` ou le `ttlId`.

**Format d’API**

```http
PUT /ttl/{DATASET_ID}
PUT /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | Identifiant du jeu de données pour lequel vous souhaitez planifier une d’expiration. |
| `{TTL_ID}` | Identifiant de l’expiration du jeu de données. |

**Requête**

La requête suivante planifie la suppression d’un jeu de données `5b020a27e7040801dedbf46e` à la fin de 2022 (heure de Greenwich). Si aucune expiration existante n’est trouvée pour le jeu de données, une nouvelle expiration sera créée. Si le jeu de données a déjà une expiration en attente, cette expiration sera mise à jour avec la nouvelle valeur `expiry`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Propriété | Description |
| --- | --- |
| `expiry` | Date et heure au format ISO 8601. Si la chaîne n’a pas de décalage de fuseau horaire explicite, le fuseau horaire est supposé être UTC. La durée de vie des données du système est définie en fonction de la valeur d’expiration fournie. Tout horodatage d’expiration précédent pour le même jeu de données est remplacé par la nouvelle valeur d’expiration que vous avez fournie. |
| `displayName` | Un nom d’affichage de la requête d’expiration. |
| `description` | Une description facultative de la requête d’expiration. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données, avec le statut HTTP 200 (OK) si une expiration préexistante a été mise à jour ou 201 (Created) en l’absence d’expiration préexistante.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | Identifiant de l’expiration du jeu de données. |
| `datasetId` | Identifiant du jeu de données auquel cette expiration s’applique. |
| `imsOrg` | Identifiant de l’organisation. |
| `status` | Statut actuel de l’expiration du jeu de données. |
| `expiry` | Date et heure planifiées de suppression du jeu de données. |
| `updatedAt` | Date et heure de la dernière mise à jour de l’expiration. |
| `updatedBy` | Dernier utilisateur à avoir mis à jour l’expiration. |

{style="table-layout:auto"}

## Annuler l’expiration d’un jeu de données {#delete}

Vous pouvez annuler l’expiration d’un jeu de données par le biais d’une requête DELETE.

>[!NOTE]
>
>Seules les expirations de jeux de données dont le statut est `pending` peuvent être annulées. La tentative d’annulation d’une expiration qui a été exécutée ou est déjà annulée renvoie une erreur HTTP 404.

**Format d’API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{EXPIRATION_ID}` | Le `ttlId` de l’expiration du jeu de données que vous souhaitez annuler. |

{style="table-layout:auto"}

**Requête**

La requête suivante annule l’expiration d’un jeu de données avec l’identifiant `SD-b16c8b48-a15a-45c8-9215-587ea89369bf` :

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 204 (No Content), et l’attribut `status` de l’expiration est défini sur `cancelled`.

## Récupérer l’historique du statut d’expiration d’un jeu de données {#retrieve-expiration-history}

Vous pouvez rechercher l’historique du statut d’expiration d’un jeu de données spécifique à l’aide du paramètre de requête `include=history` dans une requête de recherche. Le résultat comprend des informations sur la création de l’expiration du jeu de données, les mises à jour qui ont été appliquées et son annulation ou son exécution (le cas échéant). Vous pouvez également utiliser la variable `ttlId` de l’expiration du jeu de données.

**Format d’API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | L’identifiant du jeu de données dont vous souhaitez consulter l’historique des expirations. |
| `{TTL_ID}` | Identifiant de l’expiration du jeu de données. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’expiration du jeu de données, avec un tableau `history` fournissant les détails des attributs `status`, `expiry`, `updatedAt` et `updatedBy` pour chacune des mises à jour enregistrées.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | Identifiant de l’expiration du jeu de données. |
| `datasetId` | Identifiant du jeu de données auquel cette expiration s’applique. |
| `datasetName` | Le nom d’affichage du jeu de données auquel cette expiration s’applique. |
| `sandboxName` | Le nom du sandbox sous lequel se trouve le jeu de données cible. |
| `displayName` | Le nom d’affichage de la requête d’expiration. |
| `description` | Une description de la requête d’expiration. |
| `imsOrg` | Identifiant de l’organisation. |
| `history` | Répertorie l’historique des mises à jour pour l’expiration sous la forme d’un tableau d’objets, chaque objet contenant les attributs `status`, `expiry`, `updatedAt` et `updatedBy` de l’expiration au moment de la mise à jour. |

{style="table-layout:auto"}

## Annexe

### Paramètres de requête acceptés {#query-params}

Le tableau suivant décrit les paramètres de requête disponibles lorsque les [expirations des jeux de données sont répertoriées](#list) :

>[!NOTE]
>
>La variable `description`, `displayName`, et `datasetName` Les paramètres contiennent tous la possibilité d’effectuer des recherches à l’aide de valeurs LIKE. Cela signifie que vous pouvez trouver des expirations de jeux de données planifiées nommées : &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; en recherchant la chaîne &quot;Name1&quot;.

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `author` | Correspond aux expirations dont `created_by` correspond à la chaîne de recherche. Si la chaîne de recherche commence par `LIKE` ou `NOT LIKE`, le reste est traité comme un modèle de recherche SQL. Dans le cas contraire, l’intégralité de la chaîne de recherche est traitée comme une chaîne littérale qui doit correspondre exactement à l’intégralité du contenu d’un champ `created_by`. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Correspond aux expirations qui ont été annulées à tout moment dans l’intervalle indiqué. Cela s’applique même si l’expiration a été rouverte ultérieurement (en définissant une nouvelle expiration pour le même jeu de données). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Correspond aux expirations qui ont été effectuées au cours de l’intervalle spécifié. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | Correspond aux expirations qui ont été créées dans la fenêtre de 24 heures à partir de l’heure indiquée.<br><br>Notez que les dates sans heure (comme `2021-12-07`) représentent la date/heure au début de la journée. Ainsi, `createdDate=2021-12-07` fait référence à l’ensemble des expirations créées le 7 décembre 2021, de `00:00:00` à `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Correspond aux expirations qui ont été créées à l’heure indiquée ou ultérieurement. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Correspond aux expirations qui ont été créées à l’heure indiquée ou antérieurement. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | Correspond aux expirations qui s’appliquent à un jeu de données spécifique. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Correspond aux expirations dont le nom du jeu de données contient la chaîne de recherche fournie. La correspondance est insensible à la casse. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Correspond aux expirations dont le nom d’affichage contient la chaîne de recherche fournie. La correspondance est insensible à la casse. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtre les résultats selon une date d’exécution exacte, une date de fin d’exécution ou une date de début d’exécution. Ils sont utilisés pour récupérer des données ou des enregistrements associés à l’exécution d’une opération à une date spécifique, avant une date particulière ou après une date particulière. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Correspond aux expirations qui doivent être exécutées ou qui ont déjà été exécutées au cours de l’intervalle spécifié. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Nombre entier compris entre 1 et 100 qui indique le nombre maximal d’expirations à renvoyer. La valeur par défaut est 25. | `limit=50` |
| `orderBy` | La variable `orderBy` Le paramètre de requête spécifie l’ordre de tri des résultats renvoyés par l’API. Utilisez-le pour classer les données en fonction d’un ou de plusieurs champs, soit par ordre croissant (ASC), soit par ordre décroissant (DESC). Utilisez le préfixe + ou - pour désigner respectivement ASC et DESC. Les valeurs suivantes sont acceptées : `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Correspond aux expirations de jeux de données dont l’ID d’organisation correspond à celui du paramètre. Cette valeur par défaut est celle des en-têtes `x-gw-ims-org-id`, et est ignorée sauf si la requête fournit un jeton de service. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Nombre entier qui indique la page des expirations à renvoyer. | `page=3` |
| `sandboxName` | Correspond aux expirations de jeux de données dont le sandbox correspond exactement à l’argument. La valeur par défaut est le nom du sandbox dans l’en-tête `x-sandbox-name` de la requête. Utilisez `sandboxName=*` pour inclure les expirations de jeux de données de tous les sandbox. | `sandboxName=dev1` |
| `search` | Correspond aux expirations où la chaîne spécifiée correspond exactement à l’ID d’expiration ou est **contenu** dans l’un de ces champs :<br><ul><li>Création</li><li>nom d&#39;affichage</li><li>description</li><li>nom d&#39;affichage</li><li>nom du jeu de données</li></ul> | `search=TESTING` |
| `status` | Liste de statuts séparés par des virgules. Lorsqu’elle est incluse, la réponse correspond aux expirations de jeux de données dont le statut actuel fait partie de ceux répertoriés. | `status=pending,cancelled` |
| `ttlId` | Correspond à la demande d’expiration avec l’ID donné. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Comme `createdDate` / `createdFromDate` / `createdToDate`, mais correspond à l’heure de mise à jour de l’expiration d’un jeu de données plutôt qu’à l’heure de création.<br><br>Une expiration est considérée comme mise à jour à chaque modification, y compris lorsqu’elle est créée, annulée ou exécutée. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}
