---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Tâches du système de Profil - API Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: c0b059d6654a98b74be5bc6a55f360c4dc2f216b
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 78%

---


# Point de terminaison des tâches du système de Profil (supprimer des requêtes)

Adobe Experience Platform vous permet d’ingérer des données provenant de plusieurs sources et de créer des profils fiables pour les clients individuels. Les données ingérées dans Platform sont stockées dans le lac de données, ainsi que dans la banque de données de Real-time Customer Profile. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin de Profils pour supprimer les données qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, il est nécessaire d’utiliser l’API Real-time Customer Profile afin de créer une tâche de système Profile, également appelée « requête de suppression », qui peut également être modifiée, surveillée ou supprimée si nécessaire.

>[!NOTE]
>Si vous essayez de supprimer des jeux de données ou des lots du lac de données, veuillez consulter les instructions dans la [présentation du service de catalogue](../../catalog/home.md).

## Prise en main

The API endpoint used in this guide is part of the [Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Avant de continuer, consultez le guide [de](getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Affichage des requêtes de suppression

Une requête de suppression est un processus persistant asynchrone, ce qui signifie que votre organisation peut exécuter plusieurs requêtes de suppression simultanément. Pour afficher toutes les requêtes de suppression en cours d’exécution par votre organisation, vous pouvez exécuter une requête GET sur le point de terminaison `/system/jobs`.

Vous pouvez également utiliser des paramètres de requête facultatifs pour filtrer la liste des requêtes de suppression renvoyées dans la réponse. Pour utiliser plusieurs paramètres, séparez chaque paramètre à l’aide d’une esperluette (&amp;).

**Format d’API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `start` | Décalez la page des résultats renvoyée, selon l’heure de création de la requête. Exemple : *`start=4`* |
| `limit` | Limitez le nombre de résultats renvoyés. Exemple : *`limit=10`* |
| `page` | Renvoyez une page de résultats spécifique, selon l’heure de création de la requête. Exemple: ***`page=2`*** |
| `sort` | Triez les résultats selon un champ spécifique dans l’ordre croissant (*`asc`*) ou décroissant (**`desc`**). Le paramètre de tri ne fonctionne pas lors du renvoi de plusieurs pages de résultats. Exemple : `sort=batchId:asc` |

**Requête**

```shell
curl -X POST \
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
| `_page.next` | If an additional page of results exists, view the next page of results by replacing the ID value in a [lookup request](#view-a-specific-delete-request) with the `"next"` value provided. |
| `jobType` | Type de tâche en cours de création. In this case, it will always return `"DELETE"`. |
| `status` | État de la requête de suppression. Possible values are `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | An object that includes the number of records that have been processed (`"recordsProcessed"`) and the time in seconds that the request has been processing, or how long the request took to complete (`"timeTakenInSec"`). |

## Création d’une requête de suppression {#create-a-delete-request}

L’exécution d’une nouvelle requête de suppression se fait par le biais d’une requête POST au point de terminaison `/systems/jobs`, où l’identifiant du jeu de données ou du lot à supprimer est fourni dans le corps de la requête.

### Suppression d’un jeu de données

Pour supprimer un jeu de données, l’identifiant du jeu de données doit être inclus dans le corps de la requête POST. Cette action supprimera TOUTES les données d’un jeu de données. Experience Platform vous permet de supprimer des jeux de données en fonction des schémas d’enregistrement et des séries temporelles.

>[!CAUTION]
> Lorsque vous tentez de supprimer un jeu de données activé pour Profile à l’aide de l’interface utilisateur d’Experience Platform, le jeu de données est désactivé pour l’ingestion, mais il ne sera pas supprimé tant qu’une requête de suppression n’aura pas été créée à l’aide de l’API. Pour plus d’informations, reportez-vous à l’[annexe](#appendix) du présent document.

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

Une réponse réussie renvoie les détails de la requête de suppression créée, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. Le **`status`** pour la requête au moment de sa création est *`"NEW"`* jusqu’à ce qu’elle commence à être traitée. Le **`dataSetId`** contenu de la réponse doit correspondre au ***`dataSetId`*** envoyé dans la requête.

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
> La raison pour laquelle vous ne pouvez pas supprimer les lots des jeux de données basés sur des schémas d’enregistrement est que les lots de jeux de données de type enregistrement remplacent les enregistrements précédents et ne peuvent donc pas être « défaits » ni supprimés. La seule façon de supprimer l&#39;impact des lots erronés pour les jeux de données basés sur des schémas d&#39;enregistrement consiste à réassimiler le lot avec les données correctes afin de remplacer les enregistrements incorrects.

Pour plus d’informations sur le comportement des enregistrements et des séries temporelles, consultez la [section sur les comportements de données XDM](../../xdm/home.md#data-behaviors) dans la présentation du système XDM.

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

Une réponse réussie renvoie les détails de la requête de suppression créée, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. Le `"status"` pour la requête au moment de sa création est `"NEW"` jusqu’à ce qu’elle commence à être traitée. Le `"batchId"` contenu de la réponse doit correspondre au `"batchId"` envoyé dans la requête.

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
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse fournit les détails de la requête de suppression, y compris son état mis à jour. L’identifiant de la requête de suppression dans la réponse doit correspondre à celui envoyé dans le chemin de la requête.

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
| `jobType` | The type of job being created, in this case it will always return `"DELETE"`. |
| `status` | État de la requête de suppression. Possible values: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | An array that includes the number of records that have been processed (`"recordsProcessed"`) and the time in seconds that the request has been processing, or how long the request took to complete (`"timeTakenInSec"`). |

Once the delete request status is `"COMPLETED"` you can confirm that the data has been deleted by attempting to access the deleted data using the Data Access API. Pour savoir comment utiliser l’API Data Access pour accéder aux jeux de données et aux lots, consultez la [documentation sur Data Access](../../data-access/home.md).

## Suppression d’une requête de suppression

Experience Platform vous permet de supprimer une requête, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche de suppression n’a pas été terminée ou est restée bloquée en cours de traitement. Pour supprimer une requête de suppression, vous pouvez exécuter une requête DELETE sur le point de terminaison `/system/jobs` et inclure l’identifiant de la requête de suppression que vous souhaitez supprimer dans le chemin de la requête.

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

Maintenant que vous connaissez les étapes de suppression des jeux de données et des lots du magasin de Profils dans l’Experience Platform, vous pouvez supprimer en toute sécurité les données qui ont été ajoutées par erreur ou dont votre organisation n’a plus besoin. N’oubliez pas qu’une requête de suppression ne peut pas être annulée. Vous devez donc supprimer uniquement les données dont vous êtes sûr que vous n’avez pas besoin et dont vous n’aurez plus jamais besoin.

## Annexe {#appendix}

Les informations suivantes complètent le fait de supprimer un jeu de données de la banque de données Profile.

### Suppression d’un jeu de données à l’aide de l’interface utilisateur Experience Platform

Lors de l’utilisation de l’interface utilisateur Experience Platform pour supprimer un jeu de données activé pour Profile, une boîte de dialogue s’ouvre. Vous êtes invité à supprimer ce jeu de données du lac des données d’Experience Platform. Utilisez l’API des tâches de système de profils pour supprimer ce jeu de données du service Profile.

Le fait de cliquer sur **Supprimer** dans l’interface utilisateur désactive le jeu de données à des fins d’ingestion, mais NE supprime PAS automatiquement le jeu de données dans le serveur principal. Pour supprimer définitivement le jeu de données, une requête de suppression doit être créée manuellement en suivant les étapes décrites dans ce guide pour [créer une requête de suppression](#create-a-delete-request).

L’illustration suivante montre l’avertissement reçu lors d’une tentative de suppression d’un jeu de données activé par Profile à l’aide de l’interface utilisateur.

![](../images/delete-profile-dataset.png)

Pour plus d’informations sur l’utilisation des jeux de données, veuillez commencer par lire la [présentation des jeux de données](../../catalog/datasets/overview.md).