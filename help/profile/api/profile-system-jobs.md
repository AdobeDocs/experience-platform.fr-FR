---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API des tâches système de profils
type: Documentation
description: Adobe Experience Platform vous permet de supprimer un jeu de données ou un lot de la banque de profils afin de supprimer les données du profil client en temps réel qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, vous devez utiliser l’API Profile pour créer une tâche système Profile ou supprimer une requête.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
TQID: https://experienceleague.adobe.com/-x1wYB0ISg-uOuBi9VvGIIN-UnE0-7VzabSBTMB0LCo
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 33a71d0528acb39753259b5024ee9cf5ae399ca2
workflow-type: tm+mt
source-wordcount: 1212
ht-degree: 32%

---

# Point d’entrée des tâches système de profils (requêtes de suppression)

Adobe Experience Platform vous permet d’ingérer des données provenant de plusieurs sources et de créer des profils fiables pour les clients individuels. Les données ingérées dans [!DNL Experience Platform] sont stockées dans le [!DNL Data Lake]. Si les jeux de données ont été activés pour Profile, ces données sont également stockées dans le magasin de données [!DNL Real-Time Customer Profile]. Il peut parfois être nécessaire de supprimer les données de profil associées à un jeu de données de la banque de profils afin de supprimer des données qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, vous devez utiliser l’API [!DNL Real-Time Customer Profile] pour créer une tâche système [!DNL Profile], ou « requête de suppression ».

>[!NOTE]
>
>Si vous essayez de supprimer des jeux de données ou des lots du [!DNL Data Lake], consultez la [présentation du service de catalogue](../../catalog/home.md) pour plus d’informations.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de [[!DNL Real-Time Customer Profile API]](https://developer.adobe.com/experience-platform-apis/references/profile). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Affichage des requêtes de suppression {#view}

Une requête de suppression est un processus persistant asynchrone, ce qui signifie que votre organisation peut exécuter plusieurs requêtes de suppression simultanément. Pour afficher toutes les requêtes de suppression en cours d’exécution par votre organisation, vous pouvez exécuter une requête GET sur le point d’entrée `/system/jobs`.

Vous pouvez également utiliser des paramètres de requête facultatifs pour filtrer la liste des requêtes de suppression renvoyées dans la réponse. Pour utiliser plusieurs paramètres, séparez chaque paramètre à l’aide d’une esperluette (`&`).

**Format d’API**

Lors de l’utilisation de ce point d’entrée, les 100 premières tâches système sont renvoyées dans l’ordre croissant, en fonction de leur date de création.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `start` | Détermine la page de départ du jeu de résultats renvoyé. Le numéro de page est basé sur 0, ce qui signifie que `start=0` renverra des résultats à partir de 0. | `start=4` |
| `limit` | Nombre de résultats renvoyés par page. | `limit=10` |

Par exemple, si vous aviez le paramètre de requête `?start=1&limit=10`, la réponse renvoie les enregistrements 10 à 19.

**Requête**

+++ Exemple de requête pour afficher vos tâches système.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Réponse**

Une réponse réussie renvoie des informations sur la page et un tableau enfants contenant un objet pour chacune des requêtes système.

+++ Une réponse réussie pour l’affichage des requêtes système

```json
{
    "_page": {
        "pageSize": 2,
        "start": "0",
        "totalCount": 2,
        "next": 1
    },
    "children:" [
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

## Création d’une requête de suppression {#create-a-delete-request}

L’exécution d’une nouvelle requête de suppression se fait par le biais d’une requête POST au point d’entrée `/systems/jobs`, où l’identifiant du jeu de données ou du lot à supprimer est fourni dans le corps de la requête.

### Supprimer un jeu de données et les données de profil associées

Pour supprimer un jeu de données et toutes les données de profil associées au jeu de données de la banque de profils, l’identifiant du jeu de données doit être inclus dans le corps de la requête POST. Cette action supprimera TOUTES les données d’un jeu de données. [!DNL Experience Platform] vous permet de supprimer des jeux de données en fonction des schémas d’enregistrement et des séries temporelles.

**Format d’API**

```http
POST /system/jobs
```

**Requête**

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
        "dataSetId": "66a92c5910df2d1767de13f3"
      }'
```

+++

| Propriété | Description |
| -------- | ----------- |
| `dataSetId` | Identifiant du jeu de données à supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la requête système nouvellement créée, y compris un identifiant unique, généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et en vérifier l’état. La `status` de la requête au moment de sa création est `NEW` jusqu’à ce qu’elle commence à être traitée (`IN-PROGRESS`). Le dataSetId dans la réponse doit correspondre au `dataSetId` envoyé dans la requête.

+++ Réponse réussie pour la création d’une requête de suppression.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "TRUNCATE_DATASET",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "NEW",
    "properties": {
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:44:50.250006Z"
}
```

| Propriété | Description |
| -------- | ----------- |
| `requestId` | Identifiant en lecture seule généré par le système pour la tâche système. |
| `requestType` | Type de la tâche système. Puisque vous supprimez un jeu de données, cette valeur est `TRUNCATE_DATASET`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Objet contenant les identifiants du jeu de données de la tâche système. |

+++

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
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB"
      }'
```

+++

| Propriété | Description |
| -------- | ----------- |
| `datasetId` | Identifiant du jeu de données pour le lot que vous souhaitez supprimer. |
| `batchId` | L’identifiant du lot que vous souhaitez supprimer. |

**Réponse**

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
    "status": "NEW",
    "properties": {
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:44:50.250006Z"
}
```

| Propriété | Description |
| -------- | ----------- |
| `requestId` | Identifiant en lecture seule généré par le système pour la tâche système. |
| `requestType` | Type de la tâche système. Puisque vous supprimez un lot, cette valeur est `DELETE_EE_BATCH`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Un objet contenant les identifiants du lot et du jeu de données de la tâche système. |

+++

Si vous tentez de lancer une requête de suppression pour un lot de jeux de données d’enregistrement, la requête échouera.

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

+++ Exemple de requête pour afficher une tâche de profil.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie les détails de la requête système spécifiée, y compris son statut mis à jour. L’identifiant de la requête système dans la réponse doit correspondre à l’identifiant envoyé dans le chemin d’accès de la requête.

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
| `requestId` | Identifiant en lecture seule généré par le système pour la tâche système. |
| `requestType` | Type de la tâche système. Les valeurs possibles sont `BACKFILL_TTL`, `DELETE_EE_BATCH` et `TRUNCATE_DATASET`. |
| `status` | Statut de la tâche système. Les valeurs possibles sont `NEW`, `SUCCESS`, `ERROR`, `FAILED` et `IN-PROGRESS`. |
| `properties` | Un objet contenant des identifiants de lot et/ou de jeu de données de la tâche système. |

+++

Une fois que le statut de la demande de suppression est `"SUCCESS"`, vous pouvez confirmer que les données ont été supprimées en essayant d’accéder aux données supprimées à l’aide de l’API Data Access. Pour savoir comment utiliser l’API Data Access pour accéder aux jeux de données et aux lots, consultez la [documentation sur Data Access](../../data-access/home.md).

## Étapes suivantes

Maintenant que vous connaissez les étapes nécessaires à la suppression des jeux de données et des lots du [!DNL Profile store] dans [!DNL Experience Platform], vous pouvez supprimer en toute sécurité les données ajoutées par erreur ou dont votre organisation n’a plus besoin. N’oubliez pas qu’une requête de suppression ne peut pas être annulée. Vous devez donc supprimer uniquement les données dont vous êtes sûr que vous n’avez pas besoin et dont vous n’aurez plus jamais besoin.
