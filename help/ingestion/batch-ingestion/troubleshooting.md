---
keywords: Experience Platform;accueil;rubriques les plus consultées;données ingérées;dépannage;questions fréquentes;Ingestion;Ingestion par lots;ingestion par lots;
solution: Experience Platform
title: Guide de dépannage de l’ingestion par lots
description: Cette documentation vous aidera à répondre aux questions fréquentes sur les API Batch Data Ingestion d’Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 37b241f15f297263cc7aa20f382c115a2d131c7e
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 97%

---

# Guide de dépannage de l’ingestion par lots

Cette documentation vous aidera à répondre aux questions fréquentes sur les API [!DNL Batch Data Ingestion] d’Adobe Experience Platform.

## Appels API par lots

### Les lots sont-ils immédiatement actifs après réception d’un état HTTP 200 OK de l’API CompleteBatch ?

La réponse `200 OK` de l’API signifie que le lot a été accepté pour traitement. Il n’est pas actif tant qu’il n’a pas atteint son état final : Actif ou Échec.

### Une nouvelle tentative d’appel API CompleteBatch est-elle sans danger après un échec ?

Oui, vous pouvez effectuer une nouvelle tentative d’appel API en toute sécurité. Malgré l’échec, il est possible que l’opération ait effectivement réussi et que le lot ait été accepté. Toutefois, les clients sont censés disposer de mécanismes de nouvelle tentative en cas d’échec de l’API et sont, en réalité, encouragés à effectuer une nouvelle tentative. En cas de réussite de l’opération, l’API renvoie une notification de réussite, même après une nouvelle tentative.

### Quand l’API Large File Upload doit-elle être utilisée ?

La taille de fichier recommandée pour l’utilisation de l’API Large File Upload est de 256 Mo ou plus. Vous trouverez plus d’informations sur l’utilisation de l’API Large File Upload [ici](./api-overview.md#ingest-large-parquet-files).

### Pourquoi l’appel API Large File Complete échoue-t-il ?

Si des blocs d’un fichier volumineux se chevauchent ou sont manquants, le serveur répond par un état HTTP 400 Bad Request. Cela peut se produire puisqu’il est possible de charger des blocs qui se chevauchent, étant donné que les validations de plage sont effectuées lorsque le fichier est terminé, lors de l’assemblage des blocs de fichier.

## Prise en charge de l’ingestion

### Quels sont les formats d’ingestion pris en charge ?

Actuellement, Parquet et JSON sont pris en charge. Le format CSV est pris en charge sur une base héritée. Tandis que les données sont promues au format maître et que les vérifications préliminaires sont effectuées, aucune fonctionnalité moderne, telle que la conversion, le partitionnement ou la validation des lignes, n’est prise en charge.

### Où faut-il préciser le format d’entrée du lot ?

Le format d’entrée doit être spécifié au moment de la création du lot dans le payload. Vous trouverez ci-dessous un exemple de spécification du format d’entrée du lot :

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Pourquoi les données téléchargées n’apparaissent-elles pas dans le jeu de données ?

Pour que les données apparaissent dans le jeu de données, le lot doit être marqué comme terminé. Tous les fichiers à ingérer doivent être téléchargés avant de marquer le lot comme terminé. Vous trouverez ci-dessous un exemple de marquage d’un lot comme terminé :

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Comment le fichier JSON à plusieurs lignes est-il ingéré ?

Pour ingérer un fichier JSON à plusieurs lignes, l’indicateur `isMultiLineJson` doit être défini au moment de la création du lot. Voici un exemple :

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Quelle est la différence entre les lignes JSON (fichier JSON à une seule ligne) et les fichiers JSON à plusieurs lignes ?

Dans le cas des lignes JSON, il existe un objet JSON par ligne. Par exemple :

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Dans le cas d’un fichier JSON à plusieurs lignes, un objet peut occuper plusieurs lignes, tandis que tous les objets sont placés dans un tableau JSON. Par exemple :

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

Par défaut, [!DNL Batch Data Ingestion] utilise le format JSON à une seule ligne.

### L’ingestion au format CSV est-elle prise en charge ?

L’ingestion au format CSV est uniquement prise en charge pour les schémas plats. Actuellement, l’ingestion de données hiérarchiques au format CSV n’est pas prise en charge.

Pour obtenir toutes les fonctionnalités d’ingestion de données, vous devez utiliser les formats JSON ou Parquet.

### Quels types de validation sont effectués sur les données ?

Trois niveaux de validation sont effectués sur les données :

- Schéma : l’ingestion par lots permet de s’assurer que le schéma des données ingérées correspond au schéma du jeu de données.
- Type de données : l’ingestion par lots permet de s’assurer que le type de chaque champ ingéré correspond au type défini dans le schéma du jeu de données.
- Contraintes : l’ingestion par lots permet de s’assurer que les contraintes, comme « Obligatoire », « Énumération » et « format », sont correctement définies dans la définition du schéma.

### Comment remplacer un lot déjà ingéré ?

Un lot déjà ingéré peut être remplacé à l’aide de la fonctionnalité Relecture de lot. Vous trouverez plus d’informations sur la fonctionnalité Relecture de lot [ici](./api-overview.md#replay-a-batch).

### Comment surveiller l’ingestion par lots ?

Une fois qu’un lot a été signalé en vue d’une promotion, la progression de l’ingestion par lots peut être surveillée à l’aide de la requête suivante :

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Cette requête vous permettra d’obtenir une réponse similaire à celle-ci :

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{ORG_ID}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## États de lot

### Quels sont les états de lot possibles ?

Au cours de son cycle de vie, un lot peut passer par les états suivants :

| État | Données écrites au format maître | Description |
| ------ | ---------------------- | ----------- |
| Abandonné | | Le client n’a pas terminé le lot dans le délai prévu. |
| Interrompu | | Le client a explicitement demandé, via les API [!DNL Batch Data Ingestion], une opération d’abandon pour le lot spécifié. Une fois que le lot a atteint l’état Chargé, il ne peut plus être abandonné. |
| Actif/Réussite | x | Le lot a été promu de l’évaluation au format maître. Il est désormais disponible pour la consommation en aval. **Remarque :** Actif et Réussite sont interchangeables. |
| Archivé | | Le lot a été archivé dans un stockage hors ligne. |
| Échoué/Échec | | État final résultant d’une configuration incorrecte et/ou de mauvaises données. Une erreur exploitable est enregistrée, ainsi que le lot, pour permettre aux clients de corriger et de renvoyer les données. **Remarque :** Échoué et Échec sont interchangeables. |
| Inactif | x | Le lot a été promu, mais la promotion a été annulée ou a expiré. Le lot ne sera plus disponible pour la consommation en aval, mais les données sous-jacentes resteront au format maître jusqu’à ce qu’elles aient été conservées, archivées ou supprimées d’une autre manière. |
| Chargement | | Le client écrit actuellement des données pour le lot. À ce stade, le lot n’est **pas** prêt pour la promotion. |
| Chargé | | Le client a terminé l’écriture des données pour le lot. Le lot est prêt pour la promotion. |
| Conservé | | Les données ont été extraites du format maître et placées dans une archive désignée d’Adobe Data Lake. |
| Évaluation | | Le client a réussi à signaler le lot à promouvoir et les données sont en cours d’évaluation en vue de leur consommation en aval. |
| Nouvelle tentative | | Le client a signalé le lot à promouvoir, mais en raison d’une erreur, un service de surveillance des lots effectue une nouvelle tentative sur le lot. Cet état peut être utilisé pour indiquer aux clients un éventuel retard dans l’ingestion des données. |
| Bloqué | | Le client a signalé le lot à promouvoir, mais après `n` nouvelles tentatives par un service de surveillance des lots, la promotion du lot a été bloquée. |

### En quoi consiste l’état « Évaluation » des lots ?

Lorsqu’un lot se trouve dans l’état « Évaluation », cela signifie que le lot a été signalé en vue d’une promotion et que les données sont évaluées pour la consommation en aval.

### En quoi consiste l’état « Nouvelle tentative » d’un lot ?

Lorsqu’un lot se trouve dans l’état « Nouvelle tentative », cela signifie que l’ingestion des données du lot a été temporairement interrompue en raison de problèmes intermittents. Dans ce cas, aucune intervention du client n’est nécessaire.

### En quoi consiste l’état « Bloqué » d’un lot ?

Lorsqu’un lot se trouve dans l’état « Bloqué », cela signifie que [!DNL Data Ingestion Services] rencontre des difficultés à ingérer le lot et que toutes les nouvelles tentatives sont épuisées.

### En quoi consiste l’état « Chargement » d’un lot ?

Lorsqu’un lot se trouve dans l’état « Chargement », cela signifie que l’API CompleteBatch n’a pas été appelée pour promouvoir le lot.

### Existe-t-il un moyen de savoir si un lot a bien été ingéré ?

Oui, une fois que l’état du lot est &quot;Actif&quot;, le lot a été ingéré avec succès. Pour connaître l’état du lot, suivez les étapes décrites [plus haut](#how-is-batch-ingestion-monitored).

### Que se passe-t-il après l’échec d’un lot ? {#what-if-a-batch-fails}

Lorsqu’un lot échoue, le processus s’arrête et renvoie un état `Failure`. La raison de son échec peut être identifiée dans la section `errors` du payload. Vous trouverez ci-dessous des exemples d’erreurs :

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

Une fois les erreurs corrigées, le lot peut à nouveau être chargé.

## Prise en charge des lots

### Comment supprimer les lots ?

Au lieu de les supprimer directement de [!DNL Catalog], les lots doivent être supprimés à l’aide de l’une des méthodes fournies ci-dessous :

1. Si le lot est en cours, il doit être abandonné.
2. Si le lot est passé au format maître, son format doit être rétabli.

### Quelles sont les mesures disponibles au niveau des lots ?

Les mesures suivantes sont disponibles pour les lots à l’état Actif/Réussite :

| Mesure | Description |
| ------ | ----------- |
| inputByteSize | Nombre total d’octets évalués pour le traitement par [!DNL Data Ingestion Services]. |
| inputRecordSize | Nombre total de lignes évaluées pour le traitement par [!DNL Data Ingestion Services]. |
| outputByteSize | Nombre total d’octets générés par [!DNL Data Ingestion Services] vers [!DNL Data Lake]. |
| outputRecordSize | Nombre total de lignes générées par [!DNL Data Ingestion Services] vers [!DNL Data Lake]. |
| partitionCount | Nombre total de partitions écrites dans [!DNL Data Lake]. |

### Pourquoi les mesures ne sont-elles pas disponibles pour certains lots ?

Deux raisons peuvent expliquer que les mesures ne soient pas disponibles pour votre lot :

1. Le lot n’a jamais atteint l’état Actif/Réussite.
2. Le lot a été promu à l’aide d’un chemin de promotion hérité, comme l’ingestion au format CSV.

### Que signifient les différents codes d’état ?

| Code d’état | Description |
| ----------- | ----------- |
| 106 | Le fichier de jeu de données est vide. |
| 118 | Le fichier CSV contient une ligne d’en-tête vide. |
| 200 | Le lot a été accepté pour traitement et atteindra son état final : Actif ou Échec. Une fois envoyé, le lot peut être surveillé à l’aide du point d’entrée `GetBatch`. |
| 400 | Requête incorrecte. Renvoi en cas d’absence ou de chevauchement de blocs dans un lot. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
