---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de l’ingestion par lots d’Adobe Experience Platform
topic: developer guide
translation-type: tm+mt
source-git-commit: 3eaef72de2999fc088b92562c08a896d1cb08e55
workflow-type: tm+mt
source-wordcount: '2670'
ht-degree: 88%

---


# Guide de développement de l’ingestion par lots

Ce document présente de manière exhaustive l’utilisation des [API d’ingestion par lots](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

L’annexe de ce document fournit des informations sur le [formatage des données à utiliser pour l’ingestion](#data-transformation-for-batch-ingestion), y compris des exemples de fichiers de données CSV et JSON.

## Prise en main

L’ingestion de données fournit une API RESTful grâce à laquelle vous pouvez effectuer des opérations CRUD sur les types d’objets pris en charge.

Les sections suivantes fournissent des informations supplémentaires que vous devrez connaître ou dont vous devrez disposer pour passer avec succès des appels à l’API Batch Ingestion.

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Ingestion par lots](./overview.md) : vous permet d’ingérer des données dans Adobe Experience Platform sous forme de fichiers de lots.
- [[!DNL Experience Data Model] (XDM) Système](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
- [[ !Sandbox DNL]](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Les requêtes contenant un payload (POST, PUT, PATCH) peuvent requérir un en-tête `Content-Type` supplémentaire. Les valeurs acceptées propres à chaque appel sont précisées dans les paramètres d’appel.

## Types

When ingesting data, it is important to understand how [!DNL Experience Data Model] (XDM) schemas work. Pour plus d’informations sur la façon dont les types de champs XDM sont associés à différents formats, reportez-vous au [guide de développement du registre des schémas](../../xdm/api/getting-started.md).

L’ingestion de données offre une certaine souplesse : si un type ne correspond pas à ce qui se trouve dans le schéma cible, les données seront converties dans le type cible précisé. Si cette conversion est impossible, le lot échouera avec `TypeCompatibilityException`.

Par exemple, ni JSON ni CSV ne comportent de date ou de type d’horodatage. Par conséquent, ces valeurs sont exprimées au moyen de [chaînes formatées ISO 8061](https://www.iso.org/fr/iso-8601-date-and-time-format.html) (« 2018-07-10T15:05:59.000-08:00 ») ou en heure Unix formatée en millisecondes (1531263959000), et sont ensuite converties en heure d’ingestion vers le type XDM cible.

Le tableau ci-dessous illustre les conversions prises en charge lors de l’ingestion de données.

| Entrant (ligne) / Cible (colonne) | Chaîne | Octet | Court | Entier | Long | Double | Date | Date et heure | Objet | Map |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Chaîne | X | X | X | X | X | X | X | X |  |  |
| Octet | X | X | X | X | X | X |  |  |  |  |
| Court | X | X | X | X | X | X |  |  |  |  |
| Entier | X | X | X | X | X | X |  |  |  |  |
| Long | X | X | X | X | X | X | X | X |  |  |
| Double | X | X | X | X | X | X |  |  |  |  |
| Date |  |  |  |  |  |  | X |  |  |  |
| Date et heure |  |  |  |  |  |  |  | X |  |  |
| Objet |  |  |  |  |  |  |  |  | X | X |
| Map |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Les booléens et les tableaux ne peuvent pas être convertis en d’autres types.

## Contraintes d’ingestion

L’ingestion de données par lots présente certaines contraintes :
- Nombre maximal de fichiers par lot : 1 500
- Taille maximale du lot : 100 Go
- Nombre maximal de propriétés ou de champs par ligne : 10 000
- Nombre maximal de lots par minute, par utilisateur : 138

## Ingestion de fichiers JSON

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devez passer au chargement de fichiers volumineux.

### Création d’un lot

Vous devrez tout d’abord créer un lot au format JSON en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

>[!NOTE]
>
>Les exemples ci-dessous concernent le format JSON à une seule ligne. Pour ingérer un format JSON à plusieurs lignes, l’indicateur `isMultiLineJson` doit être défini. Pour plus d’informations, reportez-vous au [guide de dépannage de l’ingestion par lots](./troubleshooting.md).

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |

### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

>[!NOTE]
>
>Reportez-vous à l’annexe pour y trouver un [exemple de fichier de données JSON correctement formaté](#data-transformation-for-batch-ingestion).

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d&#39;accès au fichier correspond à l&#39;emplacement d&#39;enregistrement du fichier côté Adobe. |

**Requête**

>[!NOTE]
>
>L’API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `Users/sample-user/Downloads/sample.json`. |

**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers Parquet

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devrez passer au chargement de fichiers volumineux.

### Création d’un lot

Vous devrez tout d’abord créer un lot, avec Parquet en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Paramètre | Description |
| --------- | ------------ |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |

### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d&#39;accès au fichier correspond à l&#39;emplacement d&#39;enregistrement du fichier côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `Users/sample-user/Downloads/sample.json`. |

**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez signaler comme prêt pour être terminé. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers Parquet volumineux

>[!NOTE]
>
>Cette section explique comment charger des fichiers d’une taille supérieure à 256 Mo. Les fichiers volumineux sont chargés en blocs, puis assemblés au moyen d’un signal API.

### Création d’un lot

Vous devrez tout d’abord créer un lot, avec Parquet en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |

### Initialisation d’un fichier volumineux

Après la création du lot, vous devrez initialiser le fichier volumineux avant de charger les blocs dans le lot.

**Format d’API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{FILE_NAME}` | Le nom du fichier sur le point d’être initialisé. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
201 Created
```

### Chargement des blocs d’un fichier volumineux

Une fois le fichier créé, tous les blocs suivants peuvent être chargés en exécutant des requêtes PATCH répétées, une pour chaque section du fichier.

**Format d’API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d&#39;accès au fichier correspond à l&#39;emplacement d&#39;enregistrement du fichier côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONTENT_RANGE}` | En entiers, le début et la fin de la plage demandée. |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `Users/sample-user/Downloads/sample.json`. |


**Réponse**

```http
200 OK
```

### Terminer le fichier volumineux

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

**Format d’API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez signaler comme étant terminé. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez signaler comme étant terminé. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
201 Created
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez signaler comme étant terminé. |


**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Ingestion de fichiers CSV

Pour ingérer des fichiers CSV, vous devrez créer une classe, un schéma et un jeu de données qui prend en charge le format CSV. Pour obtenir des informations détaillées sur la création de la classe et du schéma nécessaires, suivez les instructions fournies dans le [tutoriel de création de schémas ad hoc](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous obtenez des erreurs de requêtes de taille du corps, vous devrez passer au chargement de fichiers volumineux.

### Création d’un jeu de données

Après avoir suivi les instructions ci-dessus pour créer la classe et le schéma nécessaires, vous devrez créer un jeu de données capable de prendre en charge le format CSV.

**Format d’API**

```http
POST /catalog/dataSets
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{TENANT_ID}` | Cet identifiant est utilisé pour assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation IMS. |
| `{SCHEMA_ID}` | L’identifiant du schéma que vous avez créé. |

Vous trouverez ci-dessous une explication des différentes parties de la section « fileDescription » du corps JSON :

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Paramètre | Description |
| --------- | ----------- |
| `format` | Le format du fichier maître et non pas celui du fichier d’entrée. |
| `delimiters` | Le caractère à utiliser comme délimiteur. |
| `quotes` | Le caractère à utiliser pour les citations. |
| `escapes` | Le caractère à utiliser comme caractère d’échappement. |
| `header` | Le fichier chargé **doit** contenir des en-têtes. La validation du schéma étant effectuée, cette valeur doit être définie sur « true ». En outre, les en-têtes ne doivent contenir **aucune** espace. Si votre en-tête comprend des espaces, remplacez-les par des traits de soulignement. |
| `charset` | Un champ facultatif. Les jeux de caractères « US-ASCII » et « ISO-8869-1 » sont aussi pris en charge. Si ce paramètre n’est pas renseigné, le codage UTF-8 est sélectionné par défaut. |

Le jeu de données référencé doit comporter le bloc de description de fichier mentionné ci-dessus et doit pointer vers un schéma valide dans le registre. Si ce n’est pas le cas, le fichier ne passera pas au format maître Parquet.

### Création d’un lot

Vous devrez ensuite créer un lot au format d’entrée CSV. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma lié au jeu de données fourni.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |

### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

>[!NOTE]
>
>Reportez-vous à l’annexe pour y trouver un [exemple de fichier de données CSV correctement formaté](#data-transformation-for-batch-ingestion).

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d&#39;accès au fichier correspond à l&#39;emplacement d&#39;enregistrement du fichier côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `Users/sample-user/Downloads/sample.json`. |


**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Annulation d’un lot

Il est toujours possible d’annuler un lot pendant son traitement. Une fois qu’un lot est finalisé (et que son état passe par exemple à « réussi » ou « échec »), il est impossible de l’annuler.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez annuler. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Suppression d’un lot {#delete-a-batch}

Vous pouvez supprimer un lot en exécutant la requête POST suivante avec le paramètre de requête `action=REVERT` vers l’identifiant du lot que vous souhaitez supprimer. Le lot est marqué comme « inactif », ce qui le rend éligible pour le nettoyage de la mémoire. Le lot sera collecté de manière asynchrone : il sera alors marqué comme « supprimé ».

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez supprimer. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

```http
200 OK
```

## Relecture d’un lot

Si vous souhaitez remplacer un lot déjà ingéré, vous pouvez le faire grâce à la fonctionnalité « relecture de lot ». Cette action équivaut à supprimer l’ancien lot et à en ingérer un nouveau pour le remplacer.

### Création d’un lot

Vous devrez tout d’abord créer un lot au format JSON en tant que format d’entrée. Lors de la création du lot, vous devrez fournir un identifiant de jeu de données. Vous devrez également vous assurer que tous les fichiers chargés en tant que partie intégrante du lot sont conformes au schéma XDM lié au jeu de données fourni. Vous devrez également fournir le ou les anciens lots comme référence dans la section de relecture. Dans l’exemple ci-dessous, vous effectuez la relecture de lots aux identifiants `batchIdA` et `batchIdB`.

**Format d’API**

```http
POST /batches
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Paramètre | Description |
| --------- | ----------- | 
| `{DATASET_ID}` | L’identifiant du jeu de données de référence. |

**Réponse**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot récemment créé. |
| `{DATASET_ID}` | L’identifiant du jeu de données référencé. |
| `{USER_ID}` | L’identifiant de l’utilisateur qui a créé le lot. |


### Chargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le `batchId` précisé plus haut pour charger des fichiers dans le lot. Vous pouvez charger plusieurs fichiers dans le lot.

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot dans lequel vous souhaitez effectuer le chargement. |
| `{DATASET_ID}` | L’identifiant du jeu de données de référence du lot. |
| `{FILE_NAME}` | Le nom du fichier que vous souhaitez charger. Ce chemin d&#39;accès au fichier correspond à l&#39;emplacement d&#39;enregistrement du fichier côté Adobe. |

**Requête**

>[!CAUTION]
>
>Cette API prend en charge le chargement en une seule partie. Assurez-vous que le type de contenu est bien application/octet-stream. Évitez d’employer l’option curl -F, car elle utilise par défaut une requête à parties multiples incompatible avec l’API.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Paramètre | Description |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Le chemin d’accès et le nom complets du fichier que vous tentez de charger. Ce chemin d’accès au fichier correspond au chemin d’accès au fichier local, par exemple `Users/sample-user/Downloads/sample.json`. |

**Réponse**

```http
200 OK
```

### Terminer le lot

Une fois que vous avez terminé de charger toutes les différentes parties du fichier, vous devrez signaler que les données ont été entièrement chargées et que le lot est prêt pour la promotion.

**Format d’API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous souhaitez terminer. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```http
200 OK
```

## Annexe

### Transformation des données pour l’ingestion par lots

In order to ingest a data file into [!DNL Experience Platform], the hierarchical structure of the file must comply with the [Experience Data Model (XDM)](../../xdm/home.md) schema associated with the dataset being uploaded to.

Vous trouverez des informations sur le mappage d’un fichier CSV pour être conforme à un schéma XDM dans le document traitant des [exemples de transformations](../../etl/transformations.md), ainsi qu’un exemple de fichier de données JSON correctement formaté. Les exemples de fichiers fournis dans ce document se trouvent ici :

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)