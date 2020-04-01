---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur d’API  client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


#  des tâches système (supprimer des requêtes)

Adobe Experience Platform vous permet d’assimiler des données provenant de plusieurs sources et de créer des  de fiables pour les clients individuels. Les données ingérées dans Platform sont stockées dans Data Lake, ainsi que dans le magasin de données  du client en temps réel. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin de  pour supprimer des données devenues inutiles ou ajoutées par erreur. Pour ce faire, il est nécessaire d’utiliser l’API  client en temps réel afin de créer une tâche de système de , également appelée &quot;demande de suppression&quot;, qui peut également être modifiée, surveillée ou supprimée si nécessaire.

>[!NOTE]
>Si vous essayez de supprimer des jeux de données ou des lots de Data Lake, veuillez consulter la présentation [du service de](../../catalog/home.md) catalogue pour obtenir des instructions.

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de  client en temps réel. Avant de poursuivre, consultez le guide [du développeur](getting-started.md)de l’API  client en tempsréel. En particulier, la section [de](getting-started.md#getting-started) prise en main du guide du développeur de  de comprend des liens vers des sujets connexes, un guide pour lire les exemples d’appels d’API dans ce  d’et des informations importantes sur les en-têtes requis nécessaires pour effectuer des appels vers les API de plateforme d’expérience.

##  de suppression de requêtes

Une requête de suppression est un processus asynchrone qui s’exécute depuis longtemps, ce qui signifie que votre entreprise peut exécuter plusieurs requêtes de suppression simultanément. Pour  toutes les requêtes de suppression en cours d’exécution par votre organisation, vous pouvez exécuter une requête GET sur le `/system/jobs` point de fin.

Vous pouvez également utiliser des paramètres de  facultatifs pour filtrer le des demandes de suppression renvoyées dans la réponse. Pour utiliser plusieurs paramètres, séparez chaque paramètre à l’aide d’une esperluette (&amp;).

**Format API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `start` | Décalez la page des résultats renvoyée, selon l’heure de création de la requête. Exemple: `start=4` |
| `limit` | Limitez le nombre de résultats renvoyés. Exemple: `limit=10` |
| `page` | Renvoie une page de résultats spécifique, selon l’heure de création de la requête. Exemple: `page=2` |
| `sort` | Triez les résultats selon un champ spécifique dans l’ordre croissant (`asc`) ou décroissant (`desc`). Le paramètre de tri ne fonctionne pas lors du renvoi de plusieurs pages de résultats. Exemple: `sort=batchId:asc` |

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

La réponse comprend un tableau &quot;enfants&quot; avec un objet pour chaque requête de suppression contenant les détails de cette requête.

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
| _page.count | Nombre total de requêtes. Cette réponse a été tronquée pour l&#39;espace. |
| _page.next | S’il existe une page supplémentaire de résultats, la page suivante de résultats en remplaçant la valeur ID dans une requête [de](#view-a-specific-delete-request) recherche par la valeur &quot;next&quot; fournie. |
| jobType | Type de tâche en cours de création. Dans ce cas, il renverra toujours &quot;DELETE&quot;. |
| status | Statut de la requête de suppression. Les valeurs possibles sont &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;. |
| mesures | Objet qui inclut le nombre d’enregistrements qui ont été traités (&quot;recordsProcess&quot;) et la durée en secondes pendant laquelle la requête a été traitée, ou la durée pendant laquelle la requête a pris fin (&quot;timeTakenInSec&quot;). |

## Création d’une requête de suppression {#create-a-delete-request}

Le lancement d’une nouvelle requête de suppression se fait par le biais d’une requête POST au point de `/systems/jobs` fin, où l’ID du jeu de données ou du lot à supprimer est fourni dans le corps de la requête.

### Suppression d’un jeu de données

Pour supprimer un jeu de données, l’ID de jeu de données doit être inclus dans le corps de la requête POST. Cette action supprimera TOUTES les données pour un jeu de données donné. Experience Platform vous permet de supprimer des jeux de données en fonction des  d’enregistrement et des séries chronologiques.

>[!CAUTION]
> Lorsque vous tentez de supprimer un jeu de données compatible avec  à l’aide de l’interface utilisateur de la plateforme d’expérience, le jeu de données est désactivé pour l’assimilation, mais il ne sera pas supprimé tant qu’une demande de suppression n’aura pas été créée à l’aide de l’API. Pour plus d&#39;informations, reportez-vous à l&#39; [annexe](#appendix) du présent.

**Format API**

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
| dataSetId | **(Obligatoire)** ID du jeu de données que vous souhaitez supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle requête de suppression, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et vérifier son état. La requête `status` au moment de sa création se produit `"NEW"` jusqu’à ce qu’elle commence à être traitée. Le `dataSetId` contenu de la réponse doit correspondre au `dataSetId` contenu envoyé dans la requête.

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
| id | Identifiant unique, généré par le système et en lecture seule de la demande de suppression. |
| dataSetId | ID du jeu de données, tel que spécifié dans la requête POST. |

### Suppression d’un lot

Pour supprimer un lot, l’ID du lot doit être inclus dans le corps de la requête POST. Veuillez noter que vous ne pouvez pas supprimer les lots des jeux de données en fonction des  d&#39;enregistrement. Seuls les lots des jeux de données basés sur les  de séries chronologiques peuvent être supprimés.

>[!NOTE]
> La raison pour laquelle vous ne pouvez pas supprimer les lots des jeux de données en fonction des  d’enregistrement est que les lots de jeux de données de type d’enregistrement remplacent les enregistrements précédents et ne peuvent donc pas être &quot;annulés&quot; ou supprimés. La seule façon de supprimer l’impact des lots erronés pour les jeux de données basés sur les  d’enregistrement consiste à réassimiler le lot avec les données correctes afin de remplacer les enregistrements incorrects.

Pour plus d&#39;informations sur le comportement des enregistrements et des séries chronologiques, consultez la [section sur les comportements](../../xdm/home.md#data-behaviors) de données XDM dans l&#39;aperçu du système XDM.

**Format API**

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
| batchId | **(Obligatoire)** ID du lot à supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle requête de suppression, y compris un identifiant unique généré par le système et en lecture seule pour la requête. Vous pouvez l’utiliser pour rechercher la requête et vérifier son état. Le &quot;statut&quot; de la requête au moment de sa création est &quot;NOUVEAU&quot; jusqu’à ce qu’elle commence le traitement. Le paramètre &quot;batchId&quot; de la réponse doit correspondre au paramètre &quot;batchId&quot; envoyé dans la requête.

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
| id | Identifiant unique, généré par le système et en lecture seule de la demande de suppression. |
| batchId | ID du lot, tel que spécifié dans la requête POST. |

Si vous tentez de lancer une demande de suppression pour un lot de jeux de données d’enregistrement, une erreur de niveau 400 s’affichera, comme suit :

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

##  une requête de suppression spécifique {#view-a-specific-delete-request}

Pour  une requête de suppression spécifique, y compris des détails tels que son état, vous pouvez exécuter une requête de recherche (GET) sur le point de `/system/jobs` fin et inclure l’ID de la requête de suppression dans le chemin d’accès.

**Format API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
|---|---|
| {DELETE_REQUEST_ID} | **(Obligatoire)** ID de la demande de suppression que vous souhaitez . |

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

La réponse fournit les détails de la demande de suppression, y compris son état mis à jour. L’ID de la requête de suppression dans la réponse doit correspondre à celui envoyé dans le chemin de la requête.

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
| jobType | Le type de travail en cours de création, dans ce cas, renvoie toujours &quot;DELETE&quot;. |
| status | Statut de la requête de suppression. Valeurs possibles : &quot;NOUVEAU&quot;, &quot;TRAITEMENT&quot;, &quot;TERMINÉ&quot;, &quot;ERREUR&quot;. |
| mesures | Tableau qui comprend le nombre d’enregistrements qui ont été traités (&quot;recordsProcess&quot;) et la durée en secondes pendant laquelle la requête a été traitée, ou la durée pendant laquelle la requête a pris fin (&quot;timeTakenInSec&quot;). |

Une fois la demande de suppression terminée, vous pouvez confirmer que les données ont été supprimées en tentant d’accéder aux données supprimées à l’aide de l’API d’accès aux données. Pour savoir comment utiliser l&#39;API d&#39;accès aux données pour accéder aux jeux de données et aux lots, consultez la documentation [sur l&#39;accès aux](../../data-access/home.md)données.

## Suppression d’une requête de suppression

Experience Platform vous permet de supprimer une requête précédente, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche de suppression n’a pas été terminée ou est devenue bloquée au cours de l’étape de traitement. Pour supprimer une requête de suppression, vous pouvez exécuter une requête DELETE sur le `/system/jobs` point de fin et inclure l’ID de la requête de suppression que vous souhaitez supprimer sur le chemin d’accès de la requête.

**Format API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
|---|---|
| {DELETE_REQUEST_ID} | ID de la requête de suppression que vous souhaitez supprimer. |

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

Une requête de suppression réussie renvoie HTTP Status 200 (OK) et un corps de réponse vide. Vous pouvez confirmer que la requête a été supprimée en exécutant une requête GET pour la requête de suppression par son ID. Ceci doit renvoyer un état HTTP 404 (introuvable), indiquant que la demande de suppression a été supprimée.

## Étapes suivantes

Maintenant que vous connaissez les étapes nécessaires à la suppression des jeux de données et des lots du magasin de  d’expérience, vous pouvez supprimer en toute sécurité les données ajoutées par erreur ou dont votre entreprise n’a plus besoin. N’oubliez pas qu’une demande de suppression ne peut pas être annulée. Vous devez donc supprimer uniquement les données dont vous êtes sûr que vous n’avez pas besoin maintenant et dont vous n’aurez pas besoin à l’avenir.

## Annexe {#appendix}

Les informations suivantes complètent le fait de supprimer un jeu de données du magasin de .

### Suppression d’un jeu de données à l’aide de l’interface utilisateur de la plateforme d’expérience

Lors de l’utilisation de l’interface utilisateur de la plateforme d’expérience pour supprimer un jeu de données activé pour les  de, une boîte de dialogue s’ouvre. Vous êtes invité à supprimer ce jeu de données du lac des données d’expérience. Utilisez l&#39;API &quot;Tâches  systèmes&quot; pour supprimer ce jeu de données du service .&quot;

Cliquez sur **Supprimer** dans l’interface utilisateur pour désactiver le jeu de données à des fins d’assimilation, mais NE supprime PAS automatiquement le jeu de données dans le serveur principal. Pour supprimer définitivement le jeu de données, une requête de suppression doit être créée manuellement à l’aide des étapes décrites dans ce guide pour [créer une requête](#create-a-delete-request)de suppression.

L’illustration suivante présente l’avertissement lors de la tentative de suppression d’un jeu de données compatible avec les  à l’aide de l’interface utilisateur.

![](../images/delete-profile-dataset.png)

Pour plus d&#39;informations sur l&#39;utilisation des jeux de données, veuillez commencer par lire l&#39;aperçu [des](../../catalog/datasets/overview.md)jeux de données.