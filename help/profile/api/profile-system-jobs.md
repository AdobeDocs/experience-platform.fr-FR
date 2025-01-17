---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API des tâches système de profils
type: Documentation
description: Adobe Experience Platform vous permet de supprimer un jeu de données ou un lot de la banque de profils afin de supprimer les données du profil client en temps réel qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, vous devez utiliser l’API Profile pour créer une tâche système Profile ou supprimer une requête.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 16778d0edbad4539a4ff5084a2f22ca5f08e83ec
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 35%

---

# Point d’entrée des tâches système de profils (requêtes de suppression)

>[!IMPORTANT]
>
>Les points d’entrée suivants peuvent différer entre les implémentations de Adobe Experience Platform s’exécutant sur Microsoft Azure et Amazon Web Services (AWS). Un Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la présentation multi-cloud de [Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Adobe Experience Platform vous permet d’ingérer des données provenant de plusieurs sources et de créer des profils fiables pour les clients individuels. Les données ingérées dans [!DNL Platform] sont stockées dans le [!DNL Data Lake]. Si les jeux de données ont été activés pour Profile, ces données sont également stockées dans le magasin de données [!DNL Real-Time Customer Profile]. Il peut parfois être nécessaire de supprimer les données de profil associées à un jeu de données de la banque de profils afin de supprimer des données qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, vous devez utiliser l’API [!DNL Real-Time Customer Profile] pour créer une tâche système [!DNL Profile], ou « requête de suppression ».

>[!NOTE]
>
>Si vous essayez de supprimer des jeux de données ou des lots du [!DNL Data Lake], consultez la [présentation du service de catalogue](../../catalog/home.md) pour plus d’informations.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Affichage des requêtes de suppression {#view}

Une requête de suppression est un processus persistant asynchrone, ce qui signifie que votre organisation peut exécuter plusieurs requêtes de suppression simultanément. Pour afficher toutes les requêtes de suppression en cours d’exécution par votre organisation, vous pouvez exécuter une requête GET sur le point d’entrée `/system/jobs`.

Vous pouvez également utiliser des paramètres de requête facultatifs pour filtrer la liste des requêtes de suppression renvoyées dans la réponse. Pour utiliser plusieurs paramètres, séparez chaque paramètre à l’aide d’une esperluette (`&`).

**Format d’API**

>[!AVAILABILITY]
>
>Les paramètres de requête suivants sont **uniquement** disponibles lors de l’utilisation de Platform sur Microsoft Azure.
>
>Lors de l’utilisation de ce point d’entrée sur AWS, les 100 premières tâches système sont renvoyées dans l’ordre décroissant, en fonction de leur date de création.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `start` | Décalage de la page de résultats renvoyée, en fonction de l’heure de création de la requête. | `start=4` |
| `limit` | Limitez le nombre de résultats renvoyés. | `limit=10` |
| `page` | Renvoyer une page spécifique de résultats, en fonction de l’heure de création de la requête. | `page=2` |
| `sort` | Triez les résultats selon un champ spécifique dans l’ordre croissant (`asc`) ou décroissant (`desc`). Le paramètre de tri ne fonctionne pas lors du renvoi de plusieurs pages de résultats. | `sort=batchId:asc` |

**Requête**

>[!IMPORTANT]
>
>La requête suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Exemple de requête pour afficher vos tâches système.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Vous **devez** utiliser l’en-tête de requête `x-sandbox-id` au lieu de l’en-tête de requête `x-sandbox-name` lors de l’utilisation de ce point d’entrée avec AWS.

+++ Exemple de requête pour afficher vos tâches système.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**Réponse**

>[!IMPORTANT]
>
>La réponse suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Une réponse réussie comprend un tableau « enfants » avec un objet pour chaque requête de suppression contenant les détails de cette requête.

+++ Une réponse réussie pour l’affichage des requêtes de suppression

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
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
| -------- | ----------- |
| `_page.count` | Nombre total de requêtes. Cette réponse a été tronquée pour l’espace. |
| `_page.next` | S’il existe une page de résultats supplémentaire, affichez la page de résultats suivante en remplaçant la valeur d’identifiant dans une [requête de recherche](#view-a-specific-delete-request) par la valeur d’`"next"` fournie. |
| `jobType` | Type de tâche en cours de création. Dans ce cas, il renverra toujours `"DELETE"`. |
| `status` | État de la requête de suppression. Les valeurs possibles sont `"NEW"`, `"PROCESSING"`, `"COMPLETED"` et `"ERROR"`. |
| `metrics` | Objet contenant le nombre d’enregistrements traités (`"recordsProcessed"`) et la durée, en secondes, du traitement de la requête, ou la durée nécessaire à l’exécution de la requête (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Une réponse réussie renvoie un tableau contenant un objet pour chacune des requêtes système.

+++ Une réponse réussie pour l’affichage des requêtes système

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `requestId` | Identifiant de la tâche système. |
| `requestType` | Type de la tâche système. Les valeurs possibles sont `BACKFILL_TTL`, `DELETE_EE_BATCH` et `TRUNCATE_DATASET`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Un objet contenant des identifiants de lot et/ou de jeu de données de la tâche système. |

+++

>[!ENDTABS]

## Création d’une requête de suppression {#create-a-delete-request}

L’exécution d’une nouvelle requête de suppression se fait par le biais d’une requête POST au point d’entrée `/systems/jobs`, où l’identifiant du jeu de données ou du lot à supprimer est fourni dans le corps de la requête.

### Supprimer un jeu de données et les données de profil associées

Pour supprimer un jeu de données et toutes les données de profil associées au jeu de données de la banque de profils, l’identifiant du jeu de données doit être inclus dans le corps de la requête du POST. Cette action supprimera TOUTES les données d’un jeu de données. [!DNL Experience Platform] vous permet de supprimer des jeux de données en fonction des schémas d’enregistrement et des séries temporelles.

**Format d’API**

```http
POST /system/jobs
```

**Requête**

>[!IMPORTANT]
>
>La requête suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Exemple de requête pour supprimer un jeu de données.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Propriété | Description |
| -------- | ----------- |
| `dataSetId` | Identifiant du jeu de données à supprimer. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Vous **devez** utiliser l’en-tête de requête `x-sandbox-id` au lieu de l’en-tête de requête `x-sandbox-name` lors de l’utilisation de ce point d’entrée avec AWS.

+++ Exemple de requête pour supprimer un jeu de données.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Propriété | Description |
| -------- | ----------- |
| `dataSetId` | Identifiant du jeu de données à supprimer. |

>[!ENDTABS]

**Réponse**

>[!IMPORTANT]
>
>La réponse suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Une réponse réussie renvoie les détails de la requête de suppression créée, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. Le `status` pour la requête au moment de sa création est `"NEW"` jusqu’à ce qu’elle commence à être traitée. Le `dataSetId` contenu de la réponse doit correspondre au `dataSetId` envoyé dans la requête.

+++ Réponse réussie pour la création d’une requête de suppression.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant unique généré par le système et en lecture seule pour la requête de suppression. |
| `dataSetId` | Identifiant du jeu de données, tel que spécifié dans la requête POST. |

+++

>[!TAB Amazon Web Services (AWS)]

Une réponse réussie renvoie les détails de la requête système nouvellement créée.

+++ Réponse réussie pour la création d’une requête de suppression.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Propriété | Description |
| -------- | ----------- |
| `requestId` | Identifiant de la tâche système. |
| `requestType` | Type de la tâche système. Les valeurs possibles sont `BACKFILL_TTL`, `DELETE_EE_BATCH` et `TRUNCATE_DATASET`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Un objet contenant des identifiants de lot et/ou de jeu de données de la tâche système. |

+++

>[!ENDTABS]

### Suppression d’un lot

Pour supprimer un lot, l’identifiant du lot doit être inclus dans le corps de la requête POST. Veuillez noter que vous ne pouvez pas supprimer les lots des jeux de données basés sur des schémas d’enregistrement. Seuls les lots des jeux de données basés sur des schémas de séries temporelles peuvent être supprimés.

>[!NOTE]
>
> La raison pour laquelle vous ne pouvez pas supprimer les lots des jeux de données basés sur des schémas d’enregistrement est que les lots de jeux de données de type enregistrement remplacent les enregistrements précédents et ne peuvent donc pas être « défaits » ni supprimés. La seule façon de supprimer l’impact des lots erronés pour les jeux de données basés sur des schémas d’enregistrement consiste à réingérer le lot avec les données correctes afin de remplacer les enregistrements incorrects.

Pour plus d’informations sur le comportement des enregistrements et des séries temporelles, consultez la [ section sur les comportements de données XDM](../../xdm/home.md#data-behaviors) dans la présentation de la [!DNL XDM System].

**Format d’API**

```http
POST /system/jobs
```

**Requête**

>[!IMPORTANT]
>
>La requête suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Exemple de requête de suppression d’un lot.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Propriété | Description |
| -------- | ----------- |
| `datasetId` | Identifiant du jeu de données pour le lot que vous souhaitez supprimer. |
| `batchId` | L’identifiant du lot que vous souhaitez supprimer. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Vous **devez** utiliser l’en-tête de requête `x-sandbox-id` au lieu de l’en-tête de requête `x-sandbox-name` lors de l’utilisation de ce point d’entrée avec AWS.

+++ Exemple de requête de suppression d’un lot.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Propriété | Description |
| -------- | ----------- |
| `datasetId` | Identifiant du jeu de données pour le lot que vous souhaitez supprimer. |
| `batchId` | L’identifiant du lot que vous souhaitez supprimer. |

>[!ENDTABS]

**Réponse**

>[!IMPORTANT]
>
>La réponse suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Une réponse réussie renvoie les détails de la requête de suppression créée, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. Le `"status"` pour la requête au moment de sa création est `"NEW"` jusqu’à ce qu’elle commence à être traitée. La valeur `"batchId"` dans la réponse doit correspondre à la valeur `"batchId"` envoyée dans la requête.

+++ Réponse réussie pour la création d’une requête de suppression.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant unique généré par le système et en lecture seule pour la requête de suppression. |
| `datasetId` | L’identifiant du jeu de données spécifié. |
| `batchId` | Identifiant du lot, tel que spécifié dans la requête POST. |

+++

>[!TAB Amazon Web Services (AWS)]

Une réponse réussie renvoie les détails de la requête système nouvellement créée.

+++ Réponse réussie pour la création d’une requête de suppression.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Propriété | Description |
| -------- | ----------- |
| `requestId` | Identifiant de la tâche système. |
| `requestType` | Type de la tâche système. Les valeurs possibles sont `BACKFILL_TTL`, `DELETE_EE_BATCH` et `TRUNCATE_DATASET`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Un objet contenant des identifiants de lot et/ou de jeu de données de la tâche système. |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>La fonctionnalité suivante est **uniquement** disponible lors de l’utilisation de Platform sur Microsoft Azure.

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

Pour afficher une requête de suppression spécifique, y compris des détails tels que son état, vous pouvez exécuter une requête de recherche (GET) sur le point d’entrée`/system/jobs` et inclure l’identifiant de la requête de suppression dans le chemin.

**Format d’API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | L’identifiant de la requête de suppression que vous souhaitez afficher. |

**Requête**

>[!IMPORTANT]
>
>La requête suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Exemple de requête pour afficher une tâche de profil.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Vous **devez** utiliser l’en-tête de requête `x-sandbox-id` au lieu de l’en-tête de requête `x-sandbox-name` lors de l’utilisation de ce point d’entrée avec AWS.

+++ Exemple de requête pour afficher une tâche de profil.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**Réponse**

>[!IMPORTANT]
>
>La réponse suivante diffère entre les instances Azure et AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

La réponse fournit les détails de la requête de suppression, y compris son état mis à jour. L’identifiant de la requête de suppression dans la réponse (la valeur `"id"`) doit correspondre à l’identifiant envoyé dans le chemin d’accès de la requête.

+++ Réponse réussie pour l’affichage d’une requête de suppression.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Propriétés | Description |
| ---------- | ----------- |
| `jobType` | Le type de traitement en cours de création ; dans ce cas, il renvoie toujours des `"DELETE"`. |
| `status` | État de la requête de suppression. Les valeurs possibles sont `NEW`, `PROCESSING`, `COMPLETED` et `ERROR`. |
| `metrics` | Un tableau qui inclut le nombre d’enregistrements ayant été traités (`"recordsProcessed"`) et la durée, en secondes, du traitement de la requête, ou la durée nécessaire à l’exécution de la requête (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Une réponse réussie renvoie les détails de la requête système spécifiée.

+++ Réponse réussie pour l’affichage d’une requête de suppression.

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Propriété | Description |
| -------- | ----------- |
| `requestId` | Identifiant de la tâche système. |
| `requestType` | Type de la tâche système. Les valeurs possibles sont `BACKFILL_TTL`, `DELETE_EE_BATCH` et `TRUNCATE_DATASET`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Un objet contenant des identifiants de lot et/ou de jeu de données de la tâche système. |

+++

>[!ENDTABS]

Une fois que le statut de la demande de suppression est `"COMPLETED"`, vous pouvez confirmer que les données ont été supprimées en essayant d’accéder aux données supprimées à l’aide de l’API Data Access. Pour savoir comment utiliser l’API Data Access pour accéder aux jeux de données et aux lots, consultez la [documentation sur Data Access](../../data-access/home.md).

## Suppression d’une requête de suppression

>[!AVAILABILITY]
>
>Ce point d’entrée est **uniquement** pris en charge dans l’instance Azure de Adobe Experience Platform et n’est **pas** pris en charge sur l’instance AWS.

[!DNL Experience Platform] vous permet de supprimer une requête précédente, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche de suppression n’a pas été terminée ou est restée bloquée en cours de traitement. Pour supprimer une requête de suppression, vous pouvez exécuter une requête DELETE sur le point d’entrée `/system/jobs` et inclure l’identifiant de la requête de suppression que vous souhaitez supprimer dans le chemin de la requête.

**Format d’API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | Identifiant de la requête de suppression que vous souhaitez supprimer. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une requête de suppression réussie renvoie un état HTTP 200 (OK) et un corps de réponse vide. Vous pouvez confirmer que la requête a été supprimée en exécutant une requête GET pour afficher la requête de suppression par son identifiant. Ceci doit renvoyer l’état HTTP 404 (Introuvable), indiquant que la requête de suppression a été supprimée.

## Étapes suivantes

Maintenant que vous connaissez les étapes nécessaires à la suppression des jeux de données et des lots du [!DNL Profile store] dans [!DNL Experience Platform], vous pouvez supprimer en toute sécurité les données ajoutées par erreur ou dont votre organisation n’a plus besoin. N’oubliez pas qu’une requête de suppression ne peut pas être annulée. Vous devez donc supprimer uniquement les données dont vous êtes sûr que vous n’avez pas besoin et dont vous n’aurez plus jamais besoin.
