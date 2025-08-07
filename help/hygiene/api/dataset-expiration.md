---
title: Point d’entrée de l’API d’expiration du jeu de données
description: Le point d’entrée /ttl de l’API Data Hygiene vous permet de planifier par programmation l’expiration des jeux de données dans Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 19%

---

# Point d’entrée d’expiration du jeu de données

Utilisez le point d’entrée `/ttl` dans l’API Data Hygiene pour planifier la suppression des jeux de données dans Adobe Experience Platform.

Une expiration de jeu de données est une opération de suppression différée. Le jeu de données n’est pas protégé en attendant et peut être supprimé par d’autres moyens avant son expiration planifiée.

>[!NOTE]
>
>Bien que l’expiration soit spécifiée comme un instant spécifique dans le temps, la suppression effective peut prendre jusqu’à 24 heures après l’expiration. Une fois la suppression lancée, il peut s’écouler jusqu’à sept jours avant que toutes les traces du jeu de données aient été supprimées des systèmes Experience Platform.

Avant que la suppression ne commence, vous pouvez annuler l’expiration ou modifier son heure planifiée. Pour rouvrir une expiration annulée, définissez une nouvelle expiration.

Une fois la suppression commencée, la tâche d’expiration est marquée comme `executing` et ne peut plus être modifiée. Le jeu de données peut être récupéré pendant un maximum de sept jours, mais uniquement par le biais d’une demande de service Adobe manuelle. Lors de la suppression, le lac de données, le service d’identités et le profil client en temps réel suppriment chacun le contenu du jeu de données séparément. Une fois la suppression terminée, l’expiration est marquée comme `completed`.

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

Vous pouvez répertorier toutes les expirations de jeux de données configurées pour votre organisation en effectuant une requête GET au point d’entrée `/ttl`.

Filtrez les résultats à l’aide des paramètres de requête pour renvoyer uniquement les expirations qui répondent à vos critères. Chaque résultat comprend le statut et les détails de configuration pour chaque expiration de jeu de données.

**Format d’API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMETERS}` | Une liste de paramètres de requête facultatifs avec plusieurs paramètres séparés par des caractères `&`. Les paramètres courants comprennent `limit` et `page` à des fins de pagination. Pour obtenir la liste complète des paramètres de requête pris en charge, reportez-vous à la [section annexe](#query-params) liste complète des paramètres de requête pris en charge. Les paramètres les plus couramment utilisés sont inclus ci-dessous ainsi que dans l&#39;annexe. |
| `author` | Filtrez par l’utilisateur qui a le plus récemment mis à jour ou créé l’expiration du jeu de données. Prend en charge les modèles de type SQL (par exemple, `LIKE %john%`). |
| `datasetId` | Filtrez les expirations en fonction d’un identifiant de jeu de données spécifique. |
| `datasetName` | Un filtre insensible à la casse pour les correspondances de nom de jeu de données. |
| `status` | Filtrez par une liste de statuts séparés par des virgules : `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filtrez les expirations avec une date d’expiration spécifique. |
| `limit` | Indiquez le nombre maximal de résultats à renvoyer (1-100, valeur par défaut : 25). |
| `page` | Paginer les résultats avec un index de base zéro (taille de page par défaut : 50, max. : 100). |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère toutes les expirations de jeux de données mises à jour avant le 1er août 2021 et mises à jour pour la dernière fois par un utilisateur dont le nom correspond à « Jane Doe ».

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
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Propriété | Description |
| --- | --- |
| `results` | Tableau de configurations d’expiration de jeux de données. |
| `ttlId` | Identifiant unique de la configuration de l’expiration du jeu de données. |
| `datasetId` | Identifiant unique du jeu de données associé à cette configuration. |
| `datasetName` | Nom du jeu de données. |
| `sandboxName` | Sandbox dans lequel cette expiration de jeu de données est configurée. |
| `displayName` | Nom lisible par l’utilisateur de la configuration d’expiration. |
| `description` | Description de la configuration d’expiration. |
| `imsOrg` | Identifiant d’organisation unique. |
| `status` | Statut actuel de l’expiration. Un de : `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Date et heure d’expiration planifiées (format ISO 8601). |
| `updatedAt` | Date et heure de la dernière mise à jour de cette configuration. |
| `updatedBy` | Identifiant et adresse e-mail de l’utilisateur ou du service qui a mis à jour la configuration pour la dernière fois. |
| `current_page` | Index de la page de résultats active (basé sur zéro). |
| `total_pages` | Nombre total de pages de résultats disponibles. |
| `total_count` | Nombre total d’enregistrements de configuration d’expiration de jeu de données renvoyés. |

{style="table-layout:auto"}

## Rechercher l’expiration d’un jeu de données {#lookup}

Récupérez les détails d’une configuration d’expiration de jeu de données spécifique en effectuant une requête GET avec l’identifiant d’expiration du jeu de données ou l’identifiant du jeu de données comme paramètre de chemin d’accès.

>[!IMPORTANT]
>
>Vous pouvez fournir un identifiant d’expiration de jeu de données (par exemple, `SD-xxxxxx-xxxx`) ou un identifiant de jeu de données dans le chemin d’accès . La `ttlId` dans la réponse est l’identifiant unique de l’expiration du jeu de données.

**Format d’API**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Paramètre | Description |
| --- | --- |
| `{ID}` | Identifiant unique de la configuration de l’expiration du jeu de données. Vous pouvez fournir un identifiant d’expiration de jeu de données ou un identifiant de jeu de données. |
| `include` | (Facultatif) Si elle est définie sur `history`, la réponse inclut un tableau `history` avec des événements de modification pour la configuration. |

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
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | Identifiant unique de la configuration de l’expiration du jeu de données. |
| `datasetId` | Identifiant unique du jeu de données. |
| `datasetName` | Nom du jeu de données. |
| `sandboxName` | Sandbox dans lequel l’expiration du jeu de données est configurée. |
| `displayName` | Nom lisible par l’utilisateur de la configuration d’expiration du jeu de données. |
| `description` | Description de la configuration de l’expiration du jeu de données. |
| `imsOrg` | Identifiant d’organisation unique associé à cette configuration. |
| `status` | Statut actuel de la configuration de l’expiration du jeu de données.<br>Un de : `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Date et heure d’expiration planifiées du jeu de données (format ISO 8601). |
| `updatedAt` | Date et heure de la mise à jour la plus récente. |
| `updatedBy` | Identifiant et adresse e-mail de l’utilisateur ou du service qui a mis à jour l’expiration du jeu de données pour la dernière fois. |

{style="table-layout:auto"}

### Balises d’expiration du catalogue

Lors de l’utilisation de l’[API Catalog](../../catalog/api/getting-started.md) pour rechercher les détails du jeu de données, si le jeu de données a une expiration active, il sera répertorié sous `tags.adobe/hygiene/ttl`.

Le fichier JSON suivant affiche une réponse de l’API Catalog tronquée pour un jeu de données avec une valeur d’expiration de `32503680000000`. La balise code l’expiration comme le nombre de millisecondes écoulées depuis l’époque Unix.

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

Créez une configuration d’expiration de jeu de données pour définir le moment où un jeu de données expirera et pourra être supprimé.\
Fournissez l’identifiant du jeu de données, la date ou l’heure d’expiration (au format ISO 8601), un nom d’affichage et (éventuellement) une description.

>[!NOTE]
>
>La valeur d’expiration peut être une date (AAAA-MM-JJ) ou une date et une heure (AAAA-MM-JJJ:MM:SSZ). Si vous indiquez uniquement une date, le système utilise minuit UTC (00:00:00Z) ce jour-là. La date de péremption doit être d’au moins 24 heures.

Pour créer une expiration de jeu de données, envoyez une requête POST comme illustré ci-dessous.

>[!TIP]
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
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Propriété | Description |
| --- | --- |
| `datasetId` | **Obligatoire.** Identifiant unique du jeu de données auquel appliquer l’expiration. |
| `expiry` | **Obligatoire.** Date et heure d’expiration au format ISO 8601. Cela définit la durée de vie des données dans le système. Si une seule date est fournie, la valeur par défaut est minuit UTC (00:00:00Z). La date de péremption **doit être d’au moins 24 heures**. <br>**REMARQUE** :<ul><li>La requête échoue si une expiration de jeu de données existe déjà pour le jeu de données.</li></ul> |
| `displayName` | **Obligatoire.** Nom lisible par l’utilisateur de la configuration d’expiration du jeu de données. |
| `description` | Description facultative de la configuration de l’expiration du jeu de données. |

**Réponse**

Une réponse réussie renvoie un statut HTTP 201 (Created) et la nouvelle configuration d’expiration du jeu de données.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | Identifiant unique de la configuration d’expiration du jeu de données créé. |
| `datasetId` | Identifiant unique du jeu de données. |
| `datasetName` | Nom du jeu de données. |
| `sandboxName` | Sandbox dans lequel cette expiration de jeu de données est configurée. |
| `displayName` | Nom d’affichage de la configuration de l’expiration du jeu de données. |
| `description` | Description de la configuration de l’expiration du jeu de données. |
| `imsOrg` | Identifiant d’organisation unique associé à cette configuration. |
| `status` | Statut actuel de la configuration de l’expiration du jeu de données.<br>Un de : `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Date et heure d’expiration planifiées du jeu de données. |
| `updatedAt` | Date et heure de la mise à jour la plus récente. |
| `updatedBy` | Identifiant et adresse e-mail de l’utilisateur ou du service qui a mis à jour la configuration de l’expiration du jeu de données pour la dernière fois. |

Un statut HTTP 400 (Bad Request) apparaît si une expiration de jeu de données existe déjà pour le jeu de données. Un statut HTTP 404 (Introuvable) apparaît si un jeu de données de ce type n’existe pas ou si vous n’avez pas accès au jeu de données.

## Mettre à jour une configuration d’expiration de jeu de données {#update}

Pour mettre à jour une configuration d’expiration de jeu de données existante, envoyez une requête PUT à `/ttl/DATASET_EXPIRATION_ID`. Vous pouvez uniquement mettre à jour les champs `displayName`, `description` et `expiry` de la configuration. Les mises à jour ne sont autorisées que lorsque le statut d’expiration est `pending`.

>[!NOTE]
>
>Le champ `expiry` accepte une date (AAAA-MM-JJ) ou une date et une heure (AAAA-MM-JJJ:MM:SSZ). Si une seule date est fournie, le système utilise minuit UTC (00:00:00Z) ce jour-là. La date de péremption **doit être d’au moins 24 heures**.

**Format d’API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | Identifiant unique de la configuration de l’expiration du jeu de données. **REMARQUE** : il s’agit du `ttlId` dans la réponse. |

**Requête**

La requête suivante met à jour l’expiration, le nom d’affichage et la description des `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45` d’expiration des jeux de données :

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Propriété | Description |
| --- | --- |
| `displayName` | (Facultatif) Nouveau nom lisible par l’utilisateur pour la configuration de l’expiration du jeu de données. |
| `description` | (Facultatif) Nouvelle description de la configuration de l’expiration du jeu de données. |
| `expiry` | (Facultatif) Nouvelle date ou date et heure d’expiration au format ISO 8601. Si une seule date est fournie, la valeur par défaut est minuit UTC. La date de péremption doit être **au moins 24 heures**. |

>[!NOTE]
>
>Au moins un de ces champs doit être fourni dans la requête.

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 (OK) et la configuration d’expiration du jeu de données mise à jour.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Propriété | Description |
| --- | --- |
| `ttlId` | Identifiant unique de la configuration d’expiration du jeu de données mis à jour. |
| `datasetId` | Identifiant unique du jeu de données. |
| `datasetName` | Nom du jeu de données. |
| `sandboxName` | Sandbox dans lequel cette expiration de jeu de données est configurée. |
| `displayName` | Nom d’affichage de la configuration de l’expiration du jeu de données. |
| `description` | Description de la configuration de l’expiration du jeu de données. |
| `imsOrg` | ID d’organisation associé à cette configuration. |
| `status` | Statut actuel de la configuration de l’expiration du jeu de données.<br>Un de : `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Date et heure d’expiration planifiées du jeu de données. |
| `updatedAt` | Date et heure de la mise à jour la plus récente. |
| `updatedBy` | Identifiant et adresse e-mail de l’utilisateur ou du service qui a mis à jour la configuration de l’expiration du jeu de données pour la dernière fois. |

{style="table-layout:auto"}

Une réponse infructueuse renvoie un statut HTTP 404 (Introuvable) si une telle expiration de jeu de données n’existe pas.

## Annuler l’expiration d’un jeu de données {#delete}

Annulez une configuration d’expiration de jeu de données en attente en effectuant une requête DELETE sur `/ttl/{ID}`.

>[!NOTE]
>
>Seules les expirations de jeux de données au statut `pending` peuvent être annulées. Toute tentative d’annulation d’une expiration déjà `executing`, `completed` ou `cancelled` renvoie un HTTP 400 (Bad Request).

**Format d’API**

```http
DELETE /ttl/{ID}
```

| Paramètre | Description |
| --- | --- |
| `{ID}` | Identifiant unique de la configuration de l’expiration du jeu de données. Vous pouvez fournir un identifiant d’expiration de jeu de données ou un identifiant de jeu de données. |

{style="table-layout:auto"}

**Requête**

La requête suivante annule l’expiration d’un jeu de données avec l’identifiant `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21` :

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 (OK) et la configuration d’expiration du jeu de données annulée. Notez que l’attribut `status` de l’expiration est défini sur `cancelled`.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Propriété | Description |
|---|---|
| `ttlId` | Identifiant unique de la configuration d’expiration du jeu de données supprimé. |
| `datasetId` | Identifiant unique du jeu de données. |
| `datasetName` | Nom du jeu de données. |
| `sandboxName` | Sandbox dans lequel cette expiration de jeu de données est configurée. |
| `displayName` | Nom d’affichage de la configuration de l’expiration du jeu de données. |
| `description` | Description de la configuration de l’expiration du jeu de données. |
| `imsOrg` | Identifiant d’organisation unique associé à cette configuration. |
| `status` | Statut actuel de la configuration de l’expiration du jeu de données.<br>Un de : `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Date et heure d’expiration planifiées du jeu de données. |
| `updatedAt` | Date et heure de la mise à jour la plus récente. |
| `updatedBy` | Identifiant et adresse e-mail de l’utilisateur ou du service qui a mis à jour la configuration de l’expiration du jeu de données pour la dernière fois. |

**Exemple de réponse 400 (requête incorrecte)**

Une erreur 400 se produit lors de la tentative d’annulation d’un jeu de données ayant une configuration d’expiration `executing`, `completed` ou `cancelled`.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Une erreur 404 se produit lors de la tentative d’annulation d’une expiration de jeu de données déjà `completed` ou `cancelled`.

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

