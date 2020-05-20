---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709
workflow-type: tm+mt
source-wordcount: '1506'
ht-degree: 2%

---


# Tâches du système de Profil (supprimer des requêtes)

Adobe Experience Platform vous permet d’assimiler des données provenant de plusieurs sources et de créer des profils solides pour chaque client. Les données ingérées dans Platform sont stockées dans Data Lake ainsi que dans le magasin de données du Profil client en temps réel. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin de Profils pour supprimer les données qui ne sont plus nécessaires ou qui ont été ajoutées par erreur. Pour ce faire, il est nécessaire d’utiliser l’API Profil client en temps réel pour créer une tâche système de Profil, également appelée &quot;demande de suppression&quot;, qui peut également être modifiée, surveillée ou supprimée si nécessaire.

>[!NOTE]
>Si vous essayez de supprimer des jeux de données ou des lots de Data Lake, veuillez consulter la présentation [du service de](../../catalog/home.md) catalogue pour obtenir des instructions.

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API Profil client en temps réel. Avant de continuer, consultez le guide [du développeur de l’API Profil client en temps](getting-started.md)réel. En particulier, la section [](getting-started.md#getting-started) Prise en main du guide du développeur de Profils contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

## Vue de suppression de requêtes

Une demande de suppression est un processus asynchrone à long terme, ce qui signifie que votre entreprise peut exécuter plusieurs demandes de suppression simultanément. Pour vue de toutes les requêtes de suppression en cours d’exécution par votre organisation, vous pouvez exécuter une requête GET sur le point de `/system/jobs` terminaison.

Vous pouvez également utiliser des paramètres de requête facultatifs pour filtrer la liste des requêtes de suppression renvoyées dans la réponse. Pour utiliser plusieurs paramètres, séparez chaque paramètre à l’aide d’une esperluette (&amp;).

**Format d’API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `start` | Décalez la page des résultats renvoyée, en fonction de l’heure de création de la requête. Exemple: `start=4` |
| `limit` | Limitez le nombre de résultats renvoyés. Exemple: `limit=10` |
| `page` | Renvoie une page de résultats spécifique, en fonction de l’heure de création de la requête. Exemple: `page=2` |
| `sort` | Triez les résultats selon un champ spécifique dans un ordre croissant (`asc`) ou décroissant (`desc`). Le paramètre de tri ne fonctionne pas lors du renvoi de plusieurs pages de résultats. Exemple: `sort=batchId:asc` |

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
| _page.next | S’il existe une page supplémentaire de résultats, vue la page suivante de résultats en remplaçant la valeur ID dans une demande [de](#view-a-specific-delete-request) recherche par la valeur &quot;next&quot; fournie. |
| jobType | Type de tâche en cours de création. Dans ce cas, il retournera toujours &quot;DELETE&quot;. |
| status | Statut de la demande de suppression. Les valeurs possibles sont &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;. |
| mesures | Objet qui comprend le nombre d’enregistrements traités (&quot;recordsProcédé&quot;) et la durée en secondes pendant laquelle la demande a été traitée, ou la durée de traitement de la demande (&quot;timeTakenInSec&quot;). |

## Create a delete request {#create-a-delete-request}

Le lancement d’une nouvelle demande de suppression est effectué par le biais d’une demande de post-traitement au point de `/systems/jobs` terminaison, où l’ID du jeu de données ou du lot à supprimer est fourni dans le corps de la demande.

### Suppression d’un jeu de données

Pour supprimer un jeu de données, l’ID de jeu de données doit être inclus dans le corps de la requête POST. Cette action va supprimer TOUTES les données d&#39;un jeu de données donné. Experience Platform vous permet de supprimer des jeux de données en fonction des schémas d’enregistrements et de séries chronologiques.

>[!CAUTION]
> Lorsque vous essayez de supprimer un jeu de données compatible avec les Profils à l’aide de l’interface utilisateur de la plateforme d’expérience, le jeu de données est désactivé pour l’assimilation mais ne sera pas supprimé tant qu’une demande de suppression n’aura pas été créée à l’aide de l’API. Pour plus d&#39;informations, voir l&#39; [annexe](#appendix) du présent document.

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
| dataSetId | **(Obligatoire)** ID du jeu de données que vous souhaitez supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle demande de suppression, y compris un identifiant unique, généré par le système et en lecture seule pour la demande. Vous pouvez l’utiliser pour rechercher la demande et vérifier son état. La demande `status` au moment de la création se produit `"NEW"` jusqu’à ce qu’elle commence à être traitée. Le `dataSetId` contenu de la réponse doit correspondre à celui `dataSetId` envoyé dans la demande.

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
| dataSetId | ID du jeu de données, tel que spécifié dans la demande POST. |

### Suppression d’un lot

Pour supprimer un lot, l’ID de lot doit être inclus dans le corps de la requête POST. Veuillez noter que vous ne pouvez pas supprimer les lots des jeux de données en fonction de schémas d&#39;enregistrement. Seuls les lots des jeux de données basés sur des schémas de séries chronologiques peuvent être supprimés.

>[!NOTE]
> La raison pour laquelle vous ne pouvez pas supprimer des lots pour des jeux de données basés sur des schémas d&#39;enregistrement est que les lots de jeux de données de type d&#39;enregistrement remplacent les enregistrements précédents et ne peuvent donc pas être &quot;annulés&quot; ou supprimés. La seule façon de supprimer l&#39;impact des lots erronés pour les jeux de données basés sur des schémas d&#39;enregistrement consiste à réassimiler le lot avec les données correctes afin de remplacer les enregistrements incorrects.

Pour plus d&#39;informations sur le comportement des enregistrements et des séries chronologiques, consultez la [section sur les comportements](../../xdm/home.md#data-behaviors) de données XDM dans l&#39;aperçu du système XDM.

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
| batchId | **(Obligatoire)** ID du lot à supprimer. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle demande de suppression, y compris un identifiant unique, généré par le système et en lecture seule pour la demande. Vous pouvez l’utiliser pour rechercher la demande et vérifier son état. L’&quot;état&quot; de la requête au moment de sa création est &quot;NOUVEAU&quot; jusqu’à ce qu’elle commence à être traitée. Le &quot;batchId&quot; de la réponse doit correspondre au &quot;batchId&quot; envoyé dans la demande.

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
| batchId | ID du lot, tel que spécifié dans la demande POST. |

Si vous tentez de lancer une demande de suppression pour un lot de jeux de données d&#39;enregistrements, une erreur de niveau 400 s&#39;affichera, comme suit :

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

## Vue d’une demande de suppression spécifique {#view-a-specific-delete-request}

Pour vue d’une requête de suppression spécifique, y compris des détails tels que son état, vous pouvez exécuter une requête de recherche (GET) sur le point de `/system/jobs` terminaison et inclure l’ID de la requête de suppression dans le chemin d’accès.

**Format d’API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
|---|---|
| {DELETE_REQUEST_ID} | **(Obligatoire)** ID de la demande de suppression que vous souhaitez vue. |

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
| jobType | Le type de travail en cours de création, dans ce cas, il retournera toujours &quot;DELETE&quot;. |
| status | Statut de la demande de suppression. Valeurs possibles : &quot;NOUVEAU&quot;, &quot;TRAITEMENT&quot;, &quot;TERMINÉ&quot;, &quot;ERREUR&quot;. |
| mesures | Tableau qui comprend le nombre d&#39;enregistrements traités (&quot;recordsProcess&quot;) et la durée en secondes pendant laquelle la requête a été traitée, ou la durée de traitement de la requête (&quot;timeTakenInSec&quot;). |

Une fois que l’état de la demande de suppression est &quot;TERMINÉ&quot;, vous pouvez confirmer que les données ont été supprimées en tentant d’accéder aux données supprimées à l’aide de l’API d’accès aux données. Pour savoir comment utiliser l&#39;API d&#39;accès aux données pour accéder aux jeux de données et aux lots, consultez la documentation [relative à l&#39;accès aux](../../data-access/home.md)données.

## Suppression d’une demande de suppression

Experience Platform vous permet de supprimer une requête précédente, qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche de suppression n’a pas été terminée ou s’est retrouvée bloquée dans l’étape de traitement. Pour supprimer une requête de suppression, vous pouvez exécuter une requête DELETE sur le point de `/system/jobs` terminaison et inclure l’ID de la requête de suppression que vous souhaitez supprimer sur le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Paramètre | Description |
|---|---|
| {DELETE_REQUEST_ID} | ID de la demande de suppression que vous souhaitez supprimer. |

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

Une requête de suppression réussie renvoie HTTP Status 200 (OK) et un corps de réponse vide. Vous pouvez confirmer que la demande a été supprimée en exécutant une demande GET pour la vue de la demande de suppression par son identifiant. Ceci doit renvoyer un état HTTP 404 (introuvable), indiquant que la demande de suppression a été supprimée.

## Étapes suivantes

Maintenant que vous connaissez les étapes nécessaires pour supprimer des jeux de données et des lots du magasin de Profils d’Experience Platform, vous pouvez supprimer en toute sécurité les données qui ont été ajoutées par erreur ou dont votre entreprise n’a plus besoin. N&#39;oubliez pas qu&#39;une demande de suppression ne peut pas être annulée. Par conséquent, vous ne devez supprimer que les données dont vous êtes certain que vous n&#39;avez pas besoin maintenant et dont vous n&#39;aurez pas besoin à l&#39;avenir.

## Annexe {#appendix}

Les informations suivantes complètent l&#39;action de suppression d&#39;un jeu de données du magasin de Profils.

### Suppression d’un jeu de données à l’aide de l’interface utilisateur de la plateforme d’expérience

Lors de l’utilisation de l’interface utilisateur de la plateforme d’expérience pour supprimer un jeu de données activé pour le Profil, une boîte de dialogue s’ouvre et vous demande : &quot;Voulez-vous vraiment supprimer ce jeu de données du lac des données d’expérience ? Utilisez l&#39;API &quot;tâches profil systems&quot; pour supprimer ce jeu de données du service Profil.&quot;

Cliquez sur **Supprimer** dans l&#39;interface utilisateur pour désactiver le jeu de données à assimiler, mais NE supprime PAS automatiquement le jeu de données dans le serveur principal. Pour supprimer définitivement le jeu de données, une requête de suppression doit être créée manuellement en suivant les étapes décrites dans ce guide pour [créer une requête](#create-a-delete-request)de suppression.

L’illustration suivante présente l’avertissement lors de la tentative de suppression d’un jeu de données compatible avec le Profil à l’aide de l’interface utilisateur.

![](../images/delete-profile-dataset.png)

Pour plus d&#39;informations sur l&#39;utilisation des jeux de données, veuillez commencer par lire la présentation [des](../../catalog/datasets/overview.md)jeux de données.