---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API des tâches de système de profil
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform vous permet de supprimer un jeu de données ou un lot de la banque de profils afin de supprimer les données Real-time Customer Profile devenues inutiles ou ajoutées par erreur. Pour ce faire, vous devez utiliser l’API Profile afin de créer une tâche de système Profile ou de supprimer une requête.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: ba8b62c67cdd6fa011166cc851ffc1c970108835
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 68%

---

# Point de terminaison des tâches du système Profile (requêtes de suppression)

Adobe Experience Platform vous permet d’ingérer des données provenant de plusieurs sources et de créer des profils fiables pour les clients individuels. Données ingérées dans [!DNL Platform] est stocké dans la variable [!DNL Data Lake], et si les jeux de données ont été activés pour Profile, ces données sont stockées dans la variable [!DNL Real-time Customer Profile] entrepôt de données également. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot de la banque de données Profile pour supprimer les données devenues inutiles ou ajoutées par erreur. Cela nécessite l’utilisation de la variable [!DNL Real-time Customer Profile] API pour créer une [!DNL Profile] tâche système, ou `delete request`, qui peut également être modifié, surveillé ou supprimé si nécessaire.

>[!NOTE]
>
>Si vous essayez de supprimer des jeux de données ou des lots de la variable [!DNL Data Lake], rendez-vous sur la page [Présentation du service de catalogue](../../catalog/home.md) pour plus d’informations.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Affichage des requêtes de suppression

Une requête de suppression est un processus persistant asynchrone, ce qui signifie que votre organisation peut exécuter plusieurs requêtes de suppression simultanément. Pour afficher toutes les requêtes de suppression en cours d’exécution par votre organisation, vous pouvez exécuter une requête GET sur le point de terminaison `/system/jobs`.

Vous pouvez également utiliser des paramètres de requête facultatifs pour filtrer la liste des requêtes de suppression renvoyées dans la réponse. Pour utiliser plusieurs paramètres, séparez chaque paramètre à l’aide d’une esperluette (`&`).

**Format d’API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `start` | Décalez la page des résultats renvoyée, selon l’heure de création de la requête. Exemple : `start=4` |
| `limit` | Limitez le nombre de résultats renvoyés. Exemple : `limit=10` |
| `page` | Renvoyez une page de résultats spécifique, selon l’heure de création de la requête. Exemple : `page=2` |
| `sort` | Triez les résultats selon un champ spécifique dans l’ordre croissant (`asc`) ou décroissant (`desc`). Le paramètre de tri ne fonctionne pas lors du renvoi de plusieurs pages de résultats. Exemple : `sort=batchId:asc` |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend un tableau « enfants » avec un objet pour chaque requête de suppression contenant les détails de cette requête.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Propriété | Description |
|---|---|
| `_page.count` | Nombre total de requêtes. Cette réponse a été tronquée pour l’espace. |
| `_page.next` | S’il existe une page supplémentaire de résultats, la page suivante de résultats s’affiche en remplaçant la valeur d’identifiant dans une [requête de recherche](#view-a-specific-delete-request) avec le `"next"` valeur fournie. |
| `jobType` | Type de tâche en cours de création. Dans ce cas, il renverra toujours `"DELETE"`. |
| `status` | État de la requête de suppression. Les valeurs possibles sont `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Un objet qui inclut le nombre d’enregistrements qui ont été traités (`"recordsProcessed"`) et la durée (en secondes) pendant laquelle la requête a été traitée, ou la durée (temps) de la requête (`"timeTakenInSec"`). |

## Création d’une requête de suppression {#create-a-delete-request}

L’exécution d’une nouvelle requête de suppression se fait par le biais d’une requête POST au point de terminaison `/systems/jobs`, où l’identifiant du jeu de données ou du lot à supprimer est fourni dans le corps de la requête.

### Suppression d’un jeu de données

Pour supprimer un jeu de données de la banque de profils, l’identifiant du jeu de données doit être inclus dans le corps de la requête du POST. Cette action supprimera TOUTES les données d’un jeu de données. [!DNL Experience Platform] vous permet de supprimer des jeux de données en fonction des schémas d’enregistrement et des séries temporelles.

**Format d’API**

```http
POST /system/jobs
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Propriété | Description |
|---|---|
| `dataSetId` | **(Obligatoire)** Identifiant du jeu de données que vous souhaitez supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la requête de suppression créée, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. Le `status` pour la requête au moment de sa création est `"NEW"` jusqu’à ce qu’elle commence à être traitée. Le `dataSetId` contenu de la réponse doit correspondre au `dataSetId` envoyé dans la requête.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Propriété | Description |
|---|---|
| `id` | Identifiant unique généré par le système et en lecture seule pour la requête de suppression. |
| `dataSetId` | Identifiant du jeu de données, tel que spécifié dans la requête POST. |

### Suppression d’un lot

Pour supprimer un lot, l’identifiant du lot doit être inclus dans le corps de la requête POST. Veuillez noter que vous ne pouvez pas supprimer les lots des jeux de données basés sur des schémas d’enregistrement. Seuls les lots des jeux de données basés sur des schémas de séries temporelles peuvent être supprimés.

>[!NOTE]
>
> La raison pour laquelle vous ne pouvez pas supprimer les lots des jeux de données basés sur des schémas d’enregistrement est que les lots de jeux de données de type enregistrement remplacent les enregistrements précédents et ne peuvent donc pas être « défaits » ni supprimés. La seule manière de supprimer l’impact des lots en erreur pour les jeux de données basés sur des schémas d’enregistrement consiste à ingérer à nouveau le lot avec les données correctes afin de remplacer les enregistrements incorrects.

Pour plus d’informations sur le comportement des enregistrements et des séries temporelles, veuillez consulter la section [section sur les comportements de données XDM](../../xdm/home.md#data-behaviors) dans le [!DNL XDM System] aperçu.

**Format d’API**

```http
POST /system/jobs
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Propriété | Description |
|---|---|
| `batchId` | **(Obligatoire)** Identifiant du lot que vous souhaitez supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la requête de suppression créée, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. Le `"status"` pour la requête au moment de sa création est `"NEW"` jusqu’à ce qu’elle commence à être traitée. Le `"batchId"` La valeur de la réponse doit correspondre à la variable `"batchId"` valeur envoyée dans la requête.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propriété | Description |
|---|---|
| `id` | Identifiant unique généré par le système et en lecture seule pour la requête de suppression. |
| `batchId` | Identifiant du lot, tel que spécifié dans la requête POST. |

Si vous tentez d’exécuter une requête de suppression pour un lot de jeux de données d’enregistrement, une erreur de niveau 400 s’affichera, comme suit :

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Affichage d’une requête de suppression spécifique {#view-a-specific-delete-request}

Pour afficher une requête de suppression spécifique, y compris des détails tels que son état, vous pouvez exécuter une requête de recherche (GET) sur le point de terminaison`/system/jobs` et inclure l’identifiant de la requête de suppression dans le chemin.

**Format d’API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obligatoire)** Identifiant de la requête de suppression que vous souhaitez afficher. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse fournit les détails de la requête de suppression, y compris son état mis à jour. Identifiant de la requête de suppression dans la réponse (le `"id"` ) doit correspondre à l’identifiant envoyé dans le chemin d’accès de la requête.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Propriétés | Description |
|---|---|
| `jobType` | Le type de tâche en cours de création, dans ce cas, il renverra toujours `"DELETE"`. |
| `status` | État de la requête de suppression. Valeurs possibles : `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Un tableau qui inclut le nombre d’enregistrements qui ont été traités (`"recordsProcessed"`) et la durée (en secondes) pendant laquelle la requête a été traitée, ou la durée (temps) de la requête (`"timeTakenInSec"`). |

Une fois que l’état de la requête de suppression est `"COMPLETED"` vous pouvez confirmer que les données ont été supprimées en tentant d’accéder aux données supprimées à l’aide de l’API Data Access. Pour savoir comment utiliser l’API Data Access pour accéder aux jeux de données et aux lots, consultez la [documentation sur Data Access](../../data-access/home.md).

## Suppression d’une requête de suppression

[!DNL Experience Platform] vous permet de supprimer une requête, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche de suppression n’a pas été terminée ou est restée bloquée en cours de traitement. Pour supprimer une requête de suppression, vous pouvez exécuter une requête DELETE sur le point de terminaison `/system/jobs` et inclure l’identifiant de la requête de suppression que vous souhaitez supprimer dans le chemin de la requête.

**Format d’API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
|---|---|
| {DELETE_REQUEST_ID} | Identifiant de la requête de suppression que vous souhaitez supprimer. |

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une requête de suppression réussie renvoie un état HTTP 200 (OK) et un corps de réponse vide. Vous pouvez confirmer que la requête a été supprimée en exécutant une requête GET pour afficher la requête de suppression par son identifiant. Ceci doit renvoyer l’état HTTP 404 (Introuvable), indiquant que la requête de suppression a été supprimée.

## Étapes suivantes

Maintenant que vous connaissez les étapes impliquées dans la suppression des jeux de données et des lots de la variable [!DNL Profile Store] dans [!DNL Experience Platform], vous pouvez supprimer en toute sécurité les données ajoutées par erreur ou dont votre entreprise n’a plus besoin. N’oubliez pas qu’une requête de suppression ne peut pas être annulée. Vous devez donc supprimer uniquement les données dont vous êtes sûr que vous n’avez pas besoin et dont vous n’aurez plus jamais besoin.
