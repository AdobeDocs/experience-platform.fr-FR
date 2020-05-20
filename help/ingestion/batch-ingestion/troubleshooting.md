---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage de l’administration par lots d’Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 1%

---


# Guide de dépannage de l&#39;assimilation par lot

Cette documentation vous aidera à répondre aux questions fréquentes sur les API d’administration des données par lots d’Adobe Experience Platform.

## Appels d’API par lot

### Les lots sont-ils immédiatement actifs après avoir reçu un HTTP 200 OK de l&#39;API CompleteBatch ?

La `200 OK` réponse de l’API signifie que le lot a été accepté pour traitement ; il n’est pas actif tant qu’il n’est pas transition à son état final, tel que Actif ou Échec.

### Est-il sûr de réessayer l&#39;appel API CompleteBatch après son échec ?

Oui - il est sûr de réessayer l&#39;appel d&#39;API. Malgré l’échec, il est possible que l’opération ait effectivement réussi et que le lot ait été accepté avec succès. Toutefois, les clients doivent avoir des mécanismes de nouvelle tentative en cas de défaillance de l’API et sont en fait encouragés à réessayer. Si l’opération a réussi, l’API renvoie la réussite, même après une nouvelle tentative.

### Quand l’API de téléchargement de fichiers volumineux doit-elle être utilisée ?

La taille de fichier recommandée pour l’utilisation de l’API de téléchargement de fichiers volumineux est de 256 Mo ou plus. Vous trouverez plus d&#39;informations sur l&#39;utilisation de l&#39;API de téléchargement de fichiers volumineux [ici](./api-overview.md#ingest-large-parquet-files).

### Pourquoi l&#39;appel de l&#39;API Large File Complete échoue-t-il ?

Si des segments d’un fichier volumineux se chevauchent ou sont manquants, le serveur répond par une requête HTTP 400 incorrecte. Cela peut se produire car il est possible de télécharger des blocs qui se chevauchent, car les validations de plage sont effectuées au moment de la fin du fichier, lorsque les blocs de fichier sont assemblés ensemble.

## Prise en charge des prélèvements

### Quels sont les formats d’assimilation pris en charge ?

Actuellement, Parquet et JSON sont pris en charge. Le format CSV est pris en charge sur une base héritée. Bien que les données soient promues au format maître et que les vérifications préliminaires soient effectuées, aucune fonction moderne, telle que la conversion, le partitionnement ou la validation des lignes, n’est prise en charge.

### Où doit-on spécifier le format d&#39;entrée par lot ?

Le format d’entrée doit être spécifié au moment de la création du lot dans la charge utile. Vous trouverez ci-dessous un exemple de la manière de spécifier le format d’entrée par lot :

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Comment le fichier JSON multiligne est-il ingéré ?

Pour ingérer des fichiers JSON multilignes, l’ `isMultiLineJson` indicateur doit être défini au moment de la création du lot. Vous trouverez un exemple de cette situation ci-dessous :

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Quelle est la différence entre les lignes JSON (JSON uniligne) et JSON multiligne ?

Pour les lignes JSON, il existe un objet JSON par ligne. Par exemple :

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Pour les fichiers JSON multilignes, un objet peut occuper plusieurs lignes, tandis que tous les objets sont enveloppés dans un tableau JSON. Par exemple :

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

Par défaut, l&#39;Ingestion des données par lot utilise le fichier JSON à une seule ligne.

### L’assimilation de CSV est-elle prise en charge ?

L’assimilation CSV est uniquement prise en charge pour les schémas plats. Actuellement, l’assimilation de données hiérarchiques dans le fichier CSV n’est pas prise en charge.

Pour obtenir toutes les fonctions d&#39;assimilation des données, vous devez utiliser des formats JSON ou Parquet.

### Quels types de validation sont effectués sur les données ?

Trois niveaux de validation sont effectués sur les données :

- Schéma - L&#39;Ingestion par lots permet de s&#39;assurer que le schéma des données assimilées correspond au schéma du jeu de données.
- Type de données - L&#39;Ingestion par lots garantit que le type de chaque champ assimilé correspond au type défini dans le schéma du jeu de données.
- Contraintes - L&#39;ingestion par lots garantit que les contraintes telles que &quot;Obligatoire&quot;, &quot;enum&quot; et &quot;format&quot; sont correctement définies dans la définition de schéma.

### Comment remplacer un lot déjà ingéré ?

Un lot déjà ingéré peut être remplacé par la fonction Lecture par lot. Vous trouverez plus d&#39;informations sur la relecture par lots [ici](./api-overview.md#replay-a-batch).

### Comment l&#39;assimilation par lots est-elle surveillée ?

Une fois qu&#39;un lot a été signalé pour la promotion par lot, la progression de l&#39;assimilation par lot peut être surveillée avec la demande suivante :

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Avec cette demande, vous obtiendrez une réponse similaire à celle-ci :

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
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

## États du lot

### Quels sont les états de lots possibles ?

Un lot peut, au cours de son cycle de vie, passer par les états suivants :

| État | Données écrites sur le modèle | Description |
| ------ | ---------------------- | ----------- |
| Abandonné |  | Le client n&#39;a pas pu terminer le lot dans la période prévue. |
| Abandonné |  | Le client a explicitement appelé, via les API d&#39;importation de données par lot, une opération d&#39;abandon pour le lot spécifié. Une fois qu&#39;un lot est à l&#39;état Chargé, le lot ne peut pas être abandonné. |
| Actif/Réussite | x | Le lot a été promu avec succès de l’étape à l’étape principale et est maintenant disponible pour la consommation en aval. **Remarque :** Actif et Réussite sont interchangeables. |
| Archivé |  | Le lot a été archivé en enregistrement froid. |
| Échec/échec |  | Etat de terminal résultant d’une configuration incorrecte et/ou de données incorrectes. Une erreur utilisable est enregistrée, ainsi que le lot, pour permettre aux clients de corriger et de soumettre à nouveau les données. **Remarque :** Les échecs et les échecs sont interchangeables. |
| Inactif | x | La promotion du lot a réussi, mais a été annulée ou a expiré. Le lot ne sera plus disponible pour la consommation en aval, mais les données sous-jacentes resteront dans le fichier maître jusqu&#39;à ce qu&#39;elles aient été conservées, archivées ou supprimées. |
| Chargement |  | Le client écrit actuellement des données pour le lot. Le lot **n&#39;est pas** prêt pour la promotion, à ce stade. |
| Chargé |  | Le client a terminé l&#39;écriture des données pour le lot. Le lot est prêt pour la promotion. |
| Retenue |  | Les données ont été extraites de Master et dans une archive désignée d’Adobe Data Lake. |
| Évaluation |  | Le client a réussi à signaler le lot pour promotion et les données sont mises en scène pour consommation en aval. |
| Nouvelle tentative |  | Le client a signalé le lot pour promotion, mais en raison d&#39;une erreur, le lot est de nouveau essayé par un service de surveillance par lots. Cet état peut être utilisé pour indiquer aux clients qu’il peut y avoir un retard dans l’assimilation des données. |
| Bloqué |  | Le client a signalé le lot pour promotion, mais après `n` des Reprises par un service de surveillance par lot, la promotion par lot est bloquée. |

### Que signifie &quot;évaluation&quot; pour les lots ?

Lorsqu’un lot se trouve dans la zone de transit, cela signifie que le lot a été signalé avec succès pour promotion et que les données sont mises en scène pour consommation en aval.

### Qu’est-ce que cela signifie lorsqu’un lot est &quot;Nouvelle tentative&quot; ?

Lorsqu’un lot est en &quot;nouvelle tentative&quot;, cela signifie que l’importation des données du lot a été temporairement interrompue en raison de problèmes intermittents. Dans ce cas, il n’est pas nécessaire d’intervenir auprès du client.

### Qu’est-ce que cela signifie lorsqu’un lot est &quot;bloqué&quot; ?

Lorsqu&#39;un lot est bloqué, cela signifie que Data Ingestion Services éprouve des difficultés à ingérer le lot et que toutes les Reprises sont épuisées.

### Que signifie-t-il si un lot est toujours &quot;Chargé&quot; ?

Lorsqu’un lot se trouve dans &quot;Chargement&quot;, cela signifie que l’API CompleteBatch n’a pas été appelée pour promouvoir le lot.

### Existe-t-il un moyen de savoir si un lot a été correctement assimilé ?

Une fois que l’état du lot est &quot;Actif&quot;, le lot a été correctement assimilé. Pour connaître l&#39;état du lot, suivez les étapes décrites [plus haut](#how-is-batch-ingestion-monitored).

### Que se passe-t-il après l’échec d’un lot ?

Lorsqu’un lot échoue, la raison de son échec peut être identifiée dans la `errors` section de la charge utile. Vous trouverez ci-dessous des exemples d’erreurs :

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

Une fois les erreurs corrigées, le lot peut être rechargé.

## Prise en charge par lots

### Comment supprimer les lots ?

Au lieu de supprimer directement du catalogue, les lots doivent être supprimés en utilisant l’une ou l’autre des méthodes fournies ci-dessous :

1. Si le lot est en cours, le lot doit être abandonné.
2. Si le lot est correctement maîtrisé, le lot doit être rétabli.

### Quelles mesures par lot sont disponibles ?

Les mesures au niveau du lot suivantes sont disponibles pour les lots à l’état Actif/Réussite :

| Mesure | Description |
| ------ | ----------- |
| inputByteSize | Nombre total d&#39;octets mis en scène pour le traitement des services d&#39;administration de données. |
| inputRecordSize | Nombre total de lignes intermédiaires à traiter pour Data Ingestion Services. |
| outputByteSize | Nombre total d&#39;octets sortis par Data Ingestion Services sur Data Lake. |
| outputRecordSize | Nombre total de lignes générées par Data Ingestion Services à Data Lake. |
| partitionCount | Nombre total de partitions écrites dans Data Lake. |

### Pourquoi les mesures ne sont-elles pas disponibles sur certains lots ?

Il existe deux raisons pour lesquelles les mesures peuvent ne pas être disponibles dans votre lot :

1. Le lot n&#39;a jamais atteint l&#39;état Actif/Réussite.
2. Le lot a été promu à l’aide d’un chemin de promotion hérité, tel que l’assimilation CSV.

### Que signifient les différents codes d’état ?

| Code de statut | Description |
| ----------- | ----------- |
| 106 | Le fichier de jeu de données est vide. |
| 118 | Le fichier CSV contient une rangée d’en-tête vide. |
| 200 | Le lot a été accepté pour traitement et sera transition à un état final, tel que Actif ou Échec. Une fois envoyé, le lot peut être surveillé à l’aide du point de `GetBatch` terminaison. |
| 400 | Requête incorrecte. Renvoyée si des blocs manquants ou se chevauchent dans un lot. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
