---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’assimilation partielle par lot d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: d560e8dd07e9590376728ae6575766cc382325a5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---



# Récupération partielle par lot (bêta)

L&#39;assimilation partielle par lot permet d&#39;assimiler des données contenant des erreurs, jusqu&#39;à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent intégrer toutes leurs données correctes dans Adobe Experience Platform, tandis que toutes leurs données incorrectes sont mises en lots séparément, ainsi que les raisons pour lesquelles elles ne sont pas valides.

Ce document fournit un didacticiel pour la gestion de l&#39;assimilation partielle des lots.

En outre, l&#39; [annexe](#appendix) de ce didacticiel fournit une référence pour les types d&#39;erreur d&#39;assimilation par lot partielle.

>[!IMPORTANT] Cette fonctionnalité n&#39;existe qu&#39;à l&#39;aide de l&#39;API. Veuillez contacter votre équipe pour accéder à cette fonction.

## Prise en main

Ce didacticiel nécessite une connaissance approfondie des différents services Adobe Experience Platform impliqués dans l’assimilation partielle de lots. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Importation](./overview.md)par lot : Méthode par laquelle la plate-forme ingère et stocke des données à partir de fichiers de données, tels que CSV et Parquet.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API de plateforme.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

## Activation d’un jeu de données pour l’assimilation par lots partielle dans l’API

<!-- >[!NOTE] This section describes enabling a dataset for partial batch ingestion using the API. For instructions on using the UI, please read the [enable a dataset for partial batch ingestion in the UI](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) step. -->

Vous pouvez créer un nouveau jeu de données ou modifier un jeu de données existant avec l&#39;assimilation partielle activée.

Pour créer un nouveau jeu de données, suivez les étapes du didacticiel [](../../catalog/api/create-dataset.md)Création d’un jeu de données. Une fois que vous avez atteint l’étape *Créer un jeu de données* , ajoutez le champ suivant dans le corps de la requête :

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| Propriété | Description |
| -------- | ----------- |
| `errorThresholdPercentage` | Le pourcentage d&#39;erreurs acceptables avant l&#39;ensemble du lot échoue. |

De même, pour modifier un jeu de données existant, suivez les étapes du guide [de développement](../../catalog/api/update-object.md)Catalogue.

Dans le jeu de données, vous devrez ajouter la balise décrite ci-dessus.

<!-- ## Enable a dataset for partial batch ingestion in the UI

>[!NOTE] This section describes enabling a dataset for partial batch ingestion using the UI. If you have already enabled a dataset for partial batch ingestion using the API, you can skip ahead to the next section.

To enable a dataset for partial ingestion through the Platform UI, click **Datasets** in the left navigation. You can either [create a new dataset](#create-a-new-dataset-with-partial-batch-ingestion-enabled) or [modify an existing dataset](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Create a new dataset with partial batch ingestion enabled

To create a new dataset, follow the steps in the [dataset user guide](../../catalog/datasets/user-guide.md). Once you reach the *Configure dataset* step, take note of the *Partial Ingestion* and *Error Diagnostics* fields.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error Diagnostics* toggle only appears when the *Partial Ingestion* toggle is off. This feature allows Platform to generate detailed error messages about your ingested batches. If the *Partial Ingestion* toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%.

### Modify an existing dataset to enable partial batch ingestion

To modify an existing dataset, select the dataset you want to modify. The sidebar on the right populates with information about the dataset. 

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%. -->

## Récupérer les erreurs d&#39;assimilation partielle des lots

Si les lots contiennent des échecs, vous devrez récupérer les informations d&#39;erreur sur ces échecs afin de pouvoir réingérer les données.

### Vérifier l&#39;état

Pour vérifier l&#39;état du lot assimilé, vous devez indiquer l&#39;identifiant du lot dans le chemin d&#39;une requête GET.

**Format d’API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot dont vous souhaitez vérifier l&#39;état. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur l’état du lot.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

Si le lot comporte une erreur et que les diagnostics d&#39;erreur sont activés, l&#39;état est &quot;réussite&quot; et contient plus d&#39;informations sur l&#39;erreur fournie dans un fichier d&#39;erreur téléchargeable.

## Étapes suivantes

Ce didacticiel explique comment créer ou modifier un jeu de données pour activer l&#39;assimilation par lots partielle. Pour plus d&#39;informations sur l&#39;assimilation de lots, consultez le guide [de développement sur l&#39;assimilation de](./api-overview.md)lots.

## Types d&#39;erreur d&#39;assimilation par lots partiels {#appendix}

L&#39;assimilation partielle par lot comporte quatre types d&#39;erreur différents lors de l&#39;assimilation de données.

- [Fichiers illisibles](#unreadable)
- [schémas ou en-têtes non valides](#schemas-headers)
- [Lignes non analysables](#unparsable)
- [Conversion XDM non valide](#conversion)

### Fichiers illisibles {#unreadable}

Si le lot ingéré contient des fichiers illisibles, les erreurs du lot sont jointes au lot lui-même. Pour plus d&#39;informations sur la récupération du lot en échec, consultez le guide [](../quality/retrieve-failed-batches.md)Récupération des lots en échec.

### schémas ou en-têtes non valides {#schemas-headers}

Si le lot assimilé comporte un schéma non valide ou des en-têtes non valides, les erreurs du lot sont jointes au lot lui-même. Pour plus d&#39;informations sur la récupération du lot en échec, consultez le guide [](../quality/retrieve-failed-batches.md)Récupération des lots en échec.

### Lignes non analysables {#unparsable}

Si le lot ingéré contient des lignes non analysables, les erreurs du lot sont stockées dans un fichier accessible à l&#39;aide du point de terminaison décrit ci-dessous.

**Format d’API**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot à partir duquel vous récupérez les informations d&#39;erreur. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails des lignes non analysables.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Conversion XDM non valide {#conversion}

Si le lot assimilé a des conversions XDM non valides, les erreurs du lot sont stockées dans un fichier accessible à l&#39;aide du point de terminaison suivant.

**Format d’API**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | Valeur `id` du lot à partir duquel vous récupérez les informations d&#39;erreur. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails des échecs de conversion XDM.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
