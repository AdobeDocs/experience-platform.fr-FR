---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l'assimilation partielle par lot des Adobes Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 0be45675e4a2e3308cb77a8bbe3189f09c2b6fd8
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 1%

---



# Récupération partielle par lot

L&#39;assimilation partielle par lot permet d&#39;assimiler des données contenant des erreurs, jusqu&#39;à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent intégrer toutes leurs données correctes à l’Adobe Experience Platform pendant que toutes leurs données incorrectes sont mises en lots séparément, ainsi que les raisons pour lesquelles elles ne sont pas valides.

Ce document fournit un didacticiel pour la gestion de l&#39;assimilation partielle des lots.

En outre, l&#39; [annexe](#appendix) de ce didacticiel fournit une référence pour les types d&#39;erreur d&#39;assimilation par lot partielle.

## Prise en main

Ce didacticiel nécessite une connaissance pratique des divers services d&#39;Adobe Experience Platform impliqués dans l&#39;assimilation partielle de lots. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Importation](./overview.md)par lot : Méthode qui [!DNL Platform] ingère et stocke des données à partir de fichiers de données, tels que CSV et Parquet.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer [!DNL Platform] les API.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de [!DNL Experience Platform] dépannage.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux [!DNL Platform] API, vous devez d&#39;abord suivre le didacticiel [d&#39;](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’ [!DNL Experience Platform] API, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées à des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Platform], voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

## Activation d’un lot pour l’assimilation partielle de lots dans l’API {#enable-api}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API. Pour obtenir des instructions sur l&#39;utilisation de l&#39;interface utilisateur, lisez l&#39; [étape d&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots dans l&#39;interface utilisateur](#enable-ui) .

Vous pouvez créer un nouveau lot avec l&#39;assimilation partielle activée.

Pour créer un nouveau lot, suivez les étapes décrites dans le guide [du développeur d&#39;assimilation](./api-overview.md)par lot. Une fois que vous avez atteint l’étape *Créer un lot* , ajoutez le champ suivant dans le corps de la demande :

```json
{
    ...
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
    ...
}
```

| Propriété | Description |
| -------- | ----------- |
| `enableErrorDiagnostics` | Indicateur qui permet [!DNL Platform] de générer des messages d&#39;erreur détaillés sur votre lot. |
| `partialIngestionPercentage` | Le pourcentage d&#39;erreurs acceptables avant l&#39;ensemble du lot échoue. Ainsi, dans cet exemple, un maximum de 5 % du lot peut être une erreur, avant qu’il ne soit endommagé. |


## Activation d’un lot pour l’assimilation partielle de lots dans l’interface utilisateur {#enable-ui}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;interface utilisateur. Si vous avez déjà activé un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API, vous pouvez passer à la section suivante.

Pour activer un lot pour l’assimilation partielle via l’ [!DNL Platform] interface utilisateur, vous pouvez créer un nouveau lot par le biais des connexions source, créer un nouveau lot dans un jeu de données existant ou créer un nouveau lot par le biais du flux[!UICONTROL &quot;]Mapper le fichier CSV au fichier XDM&quot;.

### Créer une connexion source {#new-source}

Pour créer une connexion à la source, suivez les étapes répertoriées dans l&#39;aperçu [des](../../sources/home.md)sources. Une fois que vous avez atteint l’étape de détail ** Flux de données, notez les champs de diagnostic *[!UICONTROL d’assimilation]* *[!UICONTROL partielle et d’]* erreur.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

La bascule d&#39;assimilation ** partielle vous permet d&#39;activer ou de désactiver l&#39;utilisation de l&#39;assimilation partielle par lot.

La bascule des diagnostics *[!UICONTROL d&#39;]* erreur n&#39;apparaît que lorsque la bascule d&#39;assimilation ** partielle est désactivée. Cette fonctionnalité permet [!DNL Platform] de générer des messages d&#39;erreur détaillés sur vos lots assimilés. Si la bascule d&#39;assimilation ** partielle est activée, les diagnostics d&#39;erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Le seuil ** d&#39;erreur vous permet de définir le pourcentage d&#39;erreurs acceptables avant que le lot entier n&#39;échoue. Par défaut, cette valeur est définie sur 5 %.

### Utiliser un jeu de données existant {#existing-dataset}

Pour utiliser un jeu de données existant, début en sélectionnant un jeu de données. La barre latérale sur la droite contient des informations sur le jeu de données.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

La bascule d&#39;assimilation ** partielle vous permet d&#39;activer ou de désactiver l&#39;utilisation de l&#39;assimilation partielle par lot.

La bascule des diagnostics *[!UICONTROL d&#39;]* erreur n&#39;apparaît que lorsque la bascule d&#39;assimilation ** partielle est désactivée. Cette fonctionnalité permet [!DNL Platform] de générer des messages d&#39;erreur détaillés sur vos lots assimilés. Si la bascule d&#39;assimilation ** partielle est activée, les diagnostics d&#39;erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Le seuil ** d&#39;erreur vous permet de définir le pourcentage d&#39;erreurs acceptables avant que le lot entier n&#39;échoue. Par défaut, cette valeur est définie sur 5 %.

Désormais, vous pouvez transférer des données à l’aide du bouton **Ajouter les données** et elles seront ingérées à l’aide de l’assimilation partielle.

### Utilisation du flux &quot;[!UICONTROL Mapper le fichier CSV au schéma]XDM&quot; {#map-flow}

Pour utiliser le flux &quot;[!UICONTROL Mapper un fichier CSV au schéma]XDM&quot;, suivez les étapes répertoriées dans le didacticiel [](../tutorials/map-a-csv-file.md)Mapper un fichier CSV. Une fois que vous avez atteint l’étape de données *de* Ajoute, prenez note des champs de diagnostic *[!UICONTROL d’assimilation]* *[!UICONTROL partielle et d’]* erreur.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

La bascule d&#39;assimilation ** partielle vous permet d&#39;activer ou de désactiver l&#39;utilisation de l&#39;assimilation partielle par lot.

La bascule des diagnostics *[!UICONTROL d&#39;]* erreur n&#39;apparaît que lorsque la bascule d&#39;assimilation ** partielle est désactivée. Cette fonctionnalité permet [!DNL Platform] de générer des messages d&#39;erreur détaillés sur vos lots assimilés. Si la bascule d&#39;assimilation ** partielle est activée, les diagnostics d&#39;erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Le seuil ** d&#39;erreur vous permet de définir le pourcentage d&#39;erreurs acceptables avant que le lot entier n&#39;échoue. Par défaut, cette valeur est définie sur 5 %.

## Récupérer les erreurs d&#39;assimilation partielle des lots {#retrieve-errors}

Si les lots contiennent des échecs, vous devrez récupérer les informations d&#39;erreur sur ces échecs afin de pouvoir réingérer les données.

### Vérifier l&#39;état {#check-status}

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
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
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

## Étapes suivantes {#next-steps}

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
