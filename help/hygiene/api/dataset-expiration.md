---
title: Point d’entrée de l’API d’expiration du jeu de données
description: Le point d’entrée /ttl de l’API Data Hygiene vous permet de planifier par programmation l’expiration des jeux de données dans Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 50%

---

# Point d’entrée d’expiration du jeu de données

Le point d’entrée `/ttl` de l’API Data Hygiene vous permet de planifier des dates d’expiration pour les jeux de données dans Adobe Experience Platform.

L’expiration d’un jeu de données n’est rien d’autre qu’une opération de suppression différée. En attendant, le jeu de données n’est pas protégé, il peut donc être supprimé par d’autres moyens avant son expiration.

>[!NOTE]
>
>Bien que l’expiration soit spécifiée comme un instant spécifique dans le temps, la suppression effective peut prendre jusqu’à 24 heures après l’expiration. Une fois la suppression lancée, il peut s’écouler jusqu’à sept jours avant que toutes les traces du jeu de données aient été supprimées des systèmes Experience Platform.

Avant que la suppression du jeu de données ne soit réellement lancée, vous pouvez annuler l’expiration ou modifier son heure de déclenchement. Après l’annulation de l’expiration d’un jeu de données, vous pouvez la rouvrir en définissant une nouvelle expiration.

Une fois que la suppression du jeu de données est lancée, sa tâche d’expiration est marquée comme étant `executing` et ne peut plus être modifiée. Le jeu de données lui-même peut être récupéré pendant un maximum de sept jours, mais uniquement par le biais d’un processus manuel initié par une demande de service Adobe. Lorsque la requête est exécutée, le lac de données, le service d’identités et le profil client en temps réel lancent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Une fois les données supprimées des trois services, la tâche d’expiration est marquée comme étant `completed`.

>[!WARNING]
>
>Si un jeu de données est défini pour expirer, vous devez modifier manuellement les flux de données susceptibles d’ingérer des données dans ce jeu, afin que vos workflows en aval ne soient pas affectés négativement.

Advanced Data Lifecycle Management prend en charge les suppressions de jeux de données via le point d’entrée d’expiration du jeu de données et les suppressions d’ID (données au niveau des lignes) à l’aide d’identités principales via le point d’entrée [workorder](./workorder.md). Vous pouvez également gérer les [expirations de jeux de données](../ui/dataset-expiration.md) et [suppressions d’enregistrements](../ui/record-delete.md) via l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez la documentation associée .

>[!NOTE]
>
>Le cycle de vie des données ne prend pas en charge la suppression de lots.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼAPI Data Hygiene. Avant de poursuivre, consultez le [guide de l’API](./overview.md) pour plus d’informations sur les en-têtes requis pour les opérations CRUD, les messages d’erreur, les collections Postman et la lecture d’exemples d’appels API.

>[!IMPORTANT]
>
>Lors d’appels à l’API Data Hygiene, vous devez utiliser l’en-tête `x-sandbox-name: {SANDBOX_NAME}` -H .

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
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie répertorie les expirations de jeux de données obtenues. L’exemple suivant a été tronqué pour des raisons d’espace.

>[!IMPORTANT]
>
>La `ttlId` de la réponse est également appelée la `{DATASET_EXPIRATION_ID}`. Tous deux font référence à l’identifiant unique de l’expiration du jeu de données.

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
| `total_count` | Le nombre d’expirations de jeux de données qui correspondaient aux paramètres de l’appel de liste. |
| `results` | Contient les détails des expirations de jeux de données renvoyées. Pour plus d’informations sur les propriétés d’une expiration de jeu de données, consultez la section de réponse pour effectuer un [appel de recherche](#lookup). |

{style="table-layout:auto"}

## Rechercher l’expiration d’un jeu de données {#lookup}

Pour rechercher une expiration de jeu de données, envoyez une requête GET avec le `{DATASET_ID}` ou le `{DATASET_EXPIRATION_ID}` .

>[!IMPORTANT]
>
>La `{DATASET_EXPIRATION_ID}` est appelée la `ttlId` dans la réponse. Tous deux font référence à l’identifiant unique de l’expiration du jeu de données.

**Format d’API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_ID}` | L’identifiant du jeu de données dont vous souhaitez rechercher l’expiration. |
| `{DATASET_EXPIRATION_ID}` | Identifiant de l’expiration du jeu de données. |

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

## Créer une expiration de jeu de données {#create}

Pour vous assurer que les données sont supprimées du système après une période spécifiée, planifiez une expiration pour un jeu de données spécifique en fournissant l’identifiant du jeu de données ainsi que la date et l’heure d’expiration au format ISO 8601.

Pour créer une expiration de jeu de données, effectuez une requête POST, comme illustré ci-dessous, puis fournissez les valeurs mentionnées ci-dessous dans la payload.

>[!NOTE]
>
>Si vous recevez une erreur 404, assurez-vous que la requête ne comporte pas de barres obliques supplémentaires. Une barre oblique de fin peut entraîner l’échec d’une requête POST.

**Format d’API**

```http
POST /ttl
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| Propriété | Description |
| --- | --- |
| `datasetId` | **Obligatoire** Identifiant du jeu de données cible pour lequel vous souhaitez planifier une expiration. |
| `expiry` | **Obligatoire** Date et heure au format ISO 8601. Si la chaîne ne comporte aucun décalage de fuseau horaire explicite, le fuseau horaire est supposé être UTC. La durée de vie des données dans le système est définie en fonction de la valeur d’expiration fournie.<br>Remarque :<ul><li>La requête échoue si une expiration de jeu de données existe déjà pour le jeu de données.</li><li>Cette date et cette heure doivent être au moins **24 heures à l&#39;avenir**.</li></ul> |
| `displayName` | Nom d’affichage facultatif de la requête d’expiration de jeu de données. |
| `description` | Une description facultative de la requête d’expiration. |

**Réponse**

Une réponse réussie renvoie un statut HTTP 201 (Created) et le nouveau statut de l’expiration du jeu de données.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
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
| `displayName` | Un nom d’affichage de la requête d’expiration. |
| `description` | Description de la requête d’expiration. |

Un statut HTTP 400 (Bad Request) apparaît si une expiration de jeu de données existe déjà pour le jeu de données. Une réponse infructueuse renvoie un statut HTTP 404 (Introuvable) si aucune expiration de jeu de données n’existe (ou si vous n’avez pas accès au jeu de données).

## Mettre à jour l’expiration d’un jeu de données {#update}

Pour mettre à jour une date d’expiration pour un jeu de données, utilisez une requête PUT et le `ttlId` . Vous pouvez mettre à jour les informations de `displayName`, de `description` et/ou de `expiry`.

>[!NOTE]
>
>Si vous modifiez la date et l’heure d’expiration, elles doivent être dans les 24 heures suivantes au moins. Ce délai imposé vous permet d’annuler ou de replanifier l’expiration et d’éviter toute perte accidentelle de données.

**Format d’API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | Identifiant de l’expiration du jeu de données que vous souhaitez modifier. Remarque : il s’agit de la `ttlId` dans la réponse. |

**Requête**

La requête suivante replanifie une `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` d’expiration de jeu de données à la fin de 2024 (heure de Greenwich). Si l’expiration du jeu de données existant est trouvée, cette expiration est mise à jour avec la nouvelle valeur de `expiry`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
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
| `expiry` | **Obligatoire** Date et heure au format ISO 8601. Si la chaîne ne comporte aucun décalage de fuseau horaire explicite, le fuseau horaire est supposé être UTC. La durée de vie des données dans le système est définie en fonction de la valeur d’expiration fournie. Tout horodatage d’expiration précédent pour le même jeu de données doit être remplacé par la nouvelle valeur d’expiration que vous avez fournie. Cette date et cette heure doivent être au moins **24 heures à l&#39;avenir**. |
| `displayName` | Un nom d’affichage de la requête d’expiration. |
| `description` | Une description facultative de la requête d’expiration. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie le nouveau statut de l’expiration du jeu de données et un statut HTTP 200 (OK) si une expiration préexistante a été mise à jour.

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

Une réponse infructueuse renvoie un statut HTTP 404 (Introuvable) si une telle expiration de jeu de données n’existe pas.

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

## Annexe

### Paramètres de requête acceptés {#query-params}

Le tableau suivant décrit les paramètres de requête disponibles lorsque les [expirations des jeux de données sont répertoriées](#list) :

>[!NOTE]
>
>Les paramètres `description`, `displayName` et `datasetName` contiennent tous la possibilité de rechercher des éléments par des valeurs LIKE. Cela signifie que vous pouvez trouver des expirations de jeux de données planifiées nommées : « Name123 », « Name183 », « DisplayName1234 » en recherchant la chaîne « Name1 ».

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `author` | Utilisez le paramètre de requête `author` pour trouver la personne qui a le plus récemment mis à jour l’expiration du jeu de données. Si aucune mise à jour n’a été effectuée depuis sa création, cela correspond au créateur initial de l’expiration. Ce paramètre correspond aux expirations pour lesquelles le champ `created_by` correspond à la chaîne de recherche.<br>Si la chaîne de recherche commence par `LIKE` ou `NOT LIKE`, le reste est traité comme un modèle de recherche SQL. Dans le cas contraire, l’intégralité de la chaîne de recherche est traitée comme une chaîne littérale qui doit correspondre exactement à l’intégralité du contenu d’un champ `created_by`. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Correspond aux expirations qui s’appliquent à un jeu de données spécifique. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Correspond aux expirations dont le nom du jeu de données contient la chaîne de recherche fournie. La correspondance n’est pas sensible à la casse. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Correspond aux expirations dont le nom d’affichage contient la chaîne de recherche fournie. La correspondance n’est pas sensible à la casse. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtre les résultats en fonction d’une date d’exécution exacte, d’une date de fin d’exécution ou d’une date de début d’exécution. Ils sont utilisés pour récupérer des données ou des enregistrements associés à l&#39;exécution d&#39;une opération à une date spécifique, avant une date particulière ou après une date particulière. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Correspond aux expirations qui se sont produites dans la fenêtre de 24 heures de la date spécifiée. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Correspond aux expirations qui doivent être exécutées ou qui ont déjà été exécutées au cours de l’intervalle spécifié. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Nombre entier compris entre 1 et 100 qui indique le nombre maximal d’expirations à renvoyer. La valeur par défaut est 25. | `limit=50` |
| `orderBy` | Le paramètre de requête `orderBy` spécifie l’ordre de tri des résultats renvoyés par l’API. Utilisez-la pour organiser les données en fonction d’un ou de plusieurs champs, par ordre croissant (ASC) ou décroissant (DESC). Utilisez le préfixe + ou - pour indiquer respectivement ASC et DESC. Les valeurs suivantes sont acceptées : `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Correspond aux expirations de jeux de données dont l’ID d’organisation correspond à celui du paramètre. Cette valeur par défaut est celle des en-têtes `x-gw-ims-org-id`, et est ignorée sauf si la requête fournit un jeton de service. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Nombre entier qui indique la page des expirations à renvoyer. | `page=3` |
| `sandboxName` | Correspond aux expirations de jeux de données dont le sandbox correspond exactement à l’argument. La valeur par défaut est le nom du sandbox dans l’en-tête `x-sandbox-name` de la requête. Utilisez `sandboxName=*` pour inclure les expirations de jeux de données de tous les sandbox. | `sandboxName=dev1` |
| `search` | Correspond aux expirations pour lesquelles la chaîne spécifiée correspond exactement à l’ID d’expiration ou est **contenue** dans l’un de ces champs :<br><ul><li>Auteur</li><li>nom d’affichage</li><li>description</li><li>nom d’affichage</li><li>nom du jeu de données</li></ul> | `search=TESTING` |
| `status` | Liste de statuts séparés par des virgules. Lorsqu’elle est incluse, la réponse correspond aux expirations de jeux de données dont le statut actuel fait partie de ceux répertoriés. | `status=pending,cancelled` |
| `ttlId` | Correspond à la demande d’expiration avec l’identifiant donné. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Correspond aux expirations qui ont été mises à jour dans la fenêtre de 24 heures de la date spécifiée. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Correspond aux expirations qui ont été mises à jour dans la fenêtre de 24 heures à partir de l’heure indiquée.<br><br>Une expiration est considérée comme mise à jour à chaque modification, y compris lorsqu’elle est créée, annulée ou exécutée. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

