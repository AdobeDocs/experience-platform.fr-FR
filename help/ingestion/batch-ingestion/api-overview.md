---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur Adobe Experience Platform Batch Ingestion
topic: developer guide
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Guide du développeur d&#39;assimilation par lot

Ce présente un aperçu complet de l&#39;utilisation des API [d&#39;assimilation de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)lot.

L’annexe de ce  fournit des informations sur le [formatage des données à utiliser pour l’assimilation](#data-transformation-for-batch-ingestion), y compris des exemples de fichiers de données CSV et JSON.

## Prise en main

L’assimilation de données fournit une API RESTful grâce à laquelle vous pouvez effectuer des opérations CRUD de base par rapport aux types d’objet pris en charge.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir appeler l&#39;API d&#39;importation par lot.

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Importation](./overview.md)par lot : Vous permet d’assimiler des données dans Adobe Experience Platform sous forme de fichiers de commandes.
- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Les requêtes qui contiennent une charge utile (POST, PUT, PATCH) peuvent nécessiter un `Content-Type` en-tête supplémentaire. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel. Les types de contenu suivants sont utilisés dans ce guide :

- Content-Type : application/json
- Content-Type : application/octet-stream

## Types

Lors de l’assimilation de données, il est important de comprendre le fonctionnement du XDM (Experience Data Model). Pour plus d&#39;informations sur la façon dont les types de champs XDM sont mappés sur différents formats, veuillez lire le [Guide](../../xdm/api/getting-started.md)du développeur du registre.

Il existe une certaine flexibilité lors de l’assimilation des données : si un type ne correspond pas à ce qui se trouve dans le  de , les données seront converties en type de exprimé.  Si ce n’est pas le cas, le lot échoue avec un `TypeCompatibilityException`.

Par exemple, ni JSON ni CSV ne comportent de date ou de type date-heure. Par conséquent, ces valeurs sont exprimées en millisecondes (153126395959 ou en millisecondes en utilisant des chaînes [formatées selon la norme](https://www.iso.org/iso-8601-date-and-time-format.html) ISO 8061 (&quot;2018-07-10T15:05:590&quot;). (9000) et sont converties au moment de l’assimilation au type XDM .

Le tableau ci-dessous présente les conversions prises en charge lors de l’assimilation de données.

| Entrant (ligne) vs (col) | Chaîne | Octet | Court | Entier | Long | Double | Date | Date-Heure | Objet | Carte |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Chaîne | X | X | X | X | X | X | X | X |  |  |
| Octet | X | X | X | X | X | X |  |  |  |  |
| Court | X | X | X | X | X | X |  |  |  |  |
| Entier | X | X | X | X | X | X |  |  |  |  |
| Long | X | X | X | X | X | X | X | X |  |  |
| Double | X | X | X | X | X | X |  |  |  |  |
| Date |  |  |  |  |  |  | X |  |  |  |
| Date-Heure |  |  |  |  |  |  |  | X |  |  |
| Objet |  |  |  |  |  |  |  |  | X | X |
| Carte |  |  |  |  |  |  |  |  | X | X |

>[!NOTE] Les booléens et les tableaux ne peuvent pas être convertis en d’autres types.

## Contraintes d&#39;insertion

L’assimilation de données par lots présente certaines contraintes :
- Nombre maximal de fichiers par lot : 1500
- Taille maximale du lot : 100 Go
- Nombre maximal de propriétés ou de champs par ligne : 10000
- Nombre maximal de lots par minute, par utilisateur : 138

## Importation de fichiers JSON

>[!NOTE] Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous demandez des erreurs de taille du corps, vous devez passer au téléchargement de fichiers volumineux.

### Créer un lot

Tout d’abord, vous devez créer un lot, avec JSON comme format d’entrée. Lors de la création du lot, vous devez fournir un ID de jeu de données. Vous devez également vous assurer que tous les fichiers téléchargés dans le cadre du lot sont conformes au XDM lié au jeu de données fourni.

>[!NOTE] Les exemples ci-dessous concernent le format JSON uniligne. Pour importer du code JSON multiligne, l’ `isMultiLineJson` indicateur doit être défini. Pour plus d&#39;informations, consultez le guide [de dépannage de l&#39;assimilation des](./troubleshooting.md)lots.

**Format API**

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
| `{DATASET_ID}` | ID du jeu de données de référence. |

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
| `{BATCH_ID}` | ID du lot nouvellement créé. |
| `{DATASET_ID}` | ID du jeu de données référencé. |

### Téléchargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le formulaire `batchId` from pour télécharger des fichiers vers le lot. Vous pouvez télécharger plusieurs fichiers dans le lot.

>[!NOTE] Voir la section de l’annexe pour un [exemple de fichier](#data-transformation-for-batch-ingestion)de données JSON correctement formaté.

**Format API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot vers lequel vous souhaitez effectuer le téléchargement. |
| `{DATASET_ID}` | ID du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à télécharger. |

**Requête**

>[!NOTE] L’API prend en charge le téléchargement en une seule partie. Assurez-vous que le type de contenu est application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | chemin d’accès complet et nom du fichier que vous tentez de télécharger. |

**Réponse**

```http
200 OK
```

### Traitement par lots complet

Une fois que vous avez terminé de télécharger toutes les différentes parties du fichier, vous devez signaler que les données ont été entièrement téléchargées et que le lot est prêt pour la promotion.

**Format API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot vers lequel vous souhaitez effectuer le téléchargement. |

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

## Fichiers de parquet d’assimilation

>[!NOTE] Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous demandez des erreurs de taille du corps, vous devrez basculer vers un transfert de fichier volumineux.

### Créer un lot

Tout d&#39;abord, vous devrez créer un lot, avec Parquet comme format d&#39;entrée. Lors de la création du lot, vous devez fournir un ID de jeu de données. Vous devez également vous assurer que tous les fichiers téléchargés dans le cadre du lot sont conformes au XDM lié au jeu de données fourni.

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
| `{DATASET_ID}` | ID du jeu de données de référence. |

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
| `{BATCH_ID}` | ID du lot nouvellement créé. |
| `{DATASET_ID}` | ID du jeu de données référencé. |
| `{USER_ID}` | ID de l’utilisateur qui a créé le lot. |

### Téléchargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le formulaire `batchId` from pour télécharger des fichiers vers le lot. Vous pouvez télécharger plusieurs fichiers dans le lot.

**Format API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot vers lequel vous souhaitez effectuer le téléchargement. |
| `{DATASET_ID}` | ID du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à télécharger. |

**Requête**

>[!CAUTION] Cette API prend en charge le téléchargement en une seule partie. Vérifiez que le type de contenu est application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | chemin d’accès complet et nom du fichier que vous tentez de télécharger. |

**Réponse**

```http
200 OK
```

### Traitement par lots complet

Une fois que vous avez terminé de télécharger toutes les différentes parties du fichier, vous devez signaler que les données ont été entièrement téléchargées et que le lot est prêt pour la promotion.

**Format API**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L&#39;ID du lot que vous souhaitez signaler est prêt pour l&#39;achèvement. |

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

## Incorporer des fichiers de parquet volumineux

>[!NOTE] Cette section explique comment télécharger des fichiers de plus de 256 Mo. Les fichiers volumineux sont téléchargés en morceaux puis assemblés via un signal API.

### Créer un lot

Tout d&#39;abord, vous devrez créer un lot, avec Parquet comme format d&#39;entrée. Lors de la création du lot, vous devez fournir un ID de jeu de données. Vous devez également vous assurer que tous les fichiers téléchargés dans le cadre du lot sont conformes au XDM lié au jeu de données fourni.

**Format API**

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
| --------- | -----------  |
| `{DATASET_ID}` | ID du jeu de données de référence. |

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
| `{BATCH_ID}` | ID du lot nouvellement créé. |
| `{DATASET_ID}` | ID du jeu de données référencé. |
| `{USER_ID}` | ID de l’utilisateur qui a créé le lot. |

### Initialiser un fichier volumineux

Après avoir créé le lot, vous devez initialiser le fichier volumineux avant de télécharger les blocs dans le lot.

**Format API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot nouvellement créé. |
| `{DATASET_ID}` | ID du jeu de données référencé. |
| `{FILE_NAME}` | Nom du fichier sur le point d’être initialisé. |

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

### Télécharger des blocs de fichiers volumineux

Maintenant que le fichier a été créé, tous les blocs suivants peuvent être téléchargés en exécutant des requêtes PATCH répétées, une pour chaque section du fichier.

**Format API**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot vers lequel vous souhaitez effectuer le téléchargement. |
| `{DATASET_ID}` | ID du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à télécharger. |

**Requête**

>[!CAUTION] Cette API prend en charge le téléchargement en une seule partie. Vérifiez que le type de contenu est application/octet-stream.

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
| `{CONTENT_RANGE}` | En nombres entiers, début et fin de la plage demandée. |
| `{FILE_PATH_AND_NAME}` | chemin d’accès complet et nom du fichier que vous tentez de télécharger. |


**Réponse**

```http
200 OK
```

### Compléter le fichier volumineux

Maintenant que vous avez créé un lot, vous pouvez utiliser le formulaire `batchId` from pour télécharger des fichiers vers le lot. Vous pouvez télécharger plusieurs fichiers dans le lot.

**Format API**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot dont vous souhaitez signaler la fin. |
| `{DATASET_ID}` | ID du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier dont vous souhaitez signaler la fin. |

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

### Traitement par lots complet

Une fois que vous avez terminé de télécharger toutes les différentes parties du fichier, vous devez signaler que les données ont été entièrement téléchargées et que le lot est prêt pour la promotion.

**Format API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | L&#39;ID du lot que vous souhaitez signaler est terminé. |


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

## Importation de fichiers CSV

Pour assimiler des fichiers CSV, vous devez créer une classe, un et un jeu de données prenant en charge le format CSV. Pour obtenir des informations détaillées sur la création de la classe et des  de nécessaires, suivez les instructions fournies dans le didacticiel [de création de](../../xdm/api/ad-hoc.md)ad hoc.

>[!NOTE] Les étapes suivantes s’appliquent aux petits fichiers (256 Mo ou moins). Si vous atteignez un délai d’expiration de passerelle ou que vous demandez des erreurs de taille du corps, vous devrez basculer vers le transfert de fichiers volumineux.

### Créer un jeu de données

Après avoir suivi les instructions ci-dessus pour créer la classe et le  de nécessaires, vous devez créer un jeu de données qui peut prendre en charge le format CSV.

**Format API**

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
| `{TENANT_ID}` | Cet identifiant permet de s’assurer que les ressources que vous créez sont correctement nommées et contenues dans votre organisation IMS. |
| `{SCHEMA_ID}` | ID du que vous avez créé. |

Vous trouverez ci-dessous une explication des différentes parties de la section &quot;fileDescription&quot; du corps JSON :

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
| `format` | Le format du fichier maîtrisé et non le format du fichier d’entrée. |
| `delimiters` | Caractère à utiliser comme délimiteur. |
| `quotes` | Caractère à utiliser pour les guillemets. |
| `escapes` | Caractère à utiliser comme caractère d’échappement. |
| `header` | Le fichier téléchargé **doit** contenir des en-têtes. La validation  étant effectuée, elle doit être définie sur true. En outre, les en-têtes peuvent **ne pas** contenir d’espaces. Si vous avez des espaces dans l’en-tête, remplacez-les par des traits de soulignement. |
| `charset` | Champ facultatif. Les autres jeux de caractères pris en charge sont &quot;US-ASCII&quot; et &quot;ISO-8869-1&quot;. Si ce paramètre n’est pas renseigné, le codage UTF-8 est pris en charge par défaut. |

Le jeu de données référencé doit comporter le bloc de description de fichier mentionné ci-dessus et doit pointer vers un valide dans le registre. Sinon, le fichier ne sera pas masqué en parquet.

### Créer un lot

Vous devrez ensuite créer un lot avec le format CSV comme format d’entrée. Lors de la création du lot, vous devez fournir un ID de jeu de données. Vous devez également vous assurer que tous les fichiers téléchargés dans le cadre du lot sont conformes au  de lié au jeu de données fourni.

**Format API**

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
| `{DATASET_ID}` | ID du jeu de données de référence. |

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
| `{BATCH_ID}` | ID du lot nouvellement créé. |
| `{DATASET_ID}` | ID du jeu de données référencé. |
| `{USER_ID}` | ID de l’utilisateur qui a créé le lot. |

### Téléchargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le formulaire `batchId` from pour télécharger des fichiers vers le lot. Vous pouvez télécharger plusieurs fichiers dans le lot.

>[!NOTE] Voir la section de l’annexe pour un [exemple de fichier](#data-transformation-for-batch-ingestion)de données CSV correctement formaté.

**Format API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot vers lequel vous souhaitez effectuer le téléchargement. |
| `{DATASET_ID}` | ID du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à télécharger. |

**Requête**

>[!CAUTION] Cette API prend en charge le téléchargement en une seule partie. Vérifiez que le type de contenu est application/octet-stream.

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
| `{FILE_PATH_AND_NAME}` | chemin d’accès complet et nom du fichier que vous tentez de télécharger. |


**Réponse**

```http
200 OK
```

### Traitement par lots complet

Une fois que vous avez terminé de télécharger toutes les différentes parties du fichier, vous devez signaler que les données ont été entièrement téléchargées et que le lot est prêt pour la promotion.

**Format API**

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

Pendant le traitement du lot, il est toujours possible de l’annuler. Toutefois, une fois qu’un lot est finalisé (par exemple, un état de réussite ou d’échec), il est impossible d’annuler le lot.

**Format API**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot à annuler. |

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

## Suppression d’un lot

Vous pouvez supprimer un lot en exécutant la requête POST suivante avec le paramètre `action=REVERT` du à l&#39;ID du lot que vous souhaitez supprimer. Le lot est marqué comme &quot;inactif&quot;, ce qui le rend éligible pour la collecte de déchets. Le lot sera collecté de manière asynchrone, puis marqué comme &quot;supprimé&quot;.

**Format API**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot à supprimer. |

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

## Réexécution d’un lot

Si vous souhaitez remplacer un lot déjà assimilé, vous pouvez le faire par &quot;relecture par lot&quot;. Cette action équivaut à supprimer l’ancien lot et à en ingérer un nouveau.

### Créer un lot

Tout d’abord, vous devez créer un lot, avec JSON comme format d’entrée. Lors de la création du lot, vous devez fournir un ID de jeu de données. Vous devez également vous assurer que tous les fichiers téléchargés dans le cadre du lot sont conformes au XDM lié au jeu de données fourni. De plus, vous devrez fournir les anciens lots comme référence dans la section de relecture. Dans l’exemple ci-dessous, vous réexécutez des lots avec des ID `batchIdA` et `batchIdB`.

**Format API**

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
| `{DATASET_ID}` | ID du jeu de données de référence. |

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
| `{BATCH_ID}` | ID du lot nouvellement créé. |
| `{DATASET_ID}` | ID du jeu de données référencé. |
| `{USER_ID}` | ID de l’utilisateur qui a créé le lot. |


### Téléchargement de fichiers

Maintenant que vous avez créé un lot, vous pouvez utiliser le formulaire `batchId` from pour télécharger des fichiers vers le lot. Vous pouvez télécharger plusieurs fichiers dans le lot.

**Format API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot vers lequel vous souhaitez effectuer le téléchargement. |
| `{DATASET_ID}` | ID du jeu de données de référence du lot. |
| `{FILE_NAME}` | Nom du fichier à télécharger. |

**Requête**

>[!CAUTION] Cette API prend en charge le téléchargement en une seule partie. Vérifiez que le type de contenu est application/octet-stream. N’utilisez pas l’option curl -F, car elle utilise par défaut une requête multipartie incompatible avec l’API.

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
| `{FILE_PATH_AND_NAME}` | chemin d’accès complet et nom du fichier que vous tentez de télécharger. |

**Réponse**

```http
200 OK
```

### Traitement par lots complet

Une fois que vous avez terminé de télécharger toutes les différentes parties du fichier, vous devez signaler que les données ont été entièrement téléchargées et que le lot est prêt pour la promotion.

**Format API**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --------- | ----------- |
| `{BATCH_ID}` | ID du lot que vous souhaitez terminer. |

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

### Transformation des données pour l’assimilation par lots

Pour importer un fichier de données dans la plateforme d’expérience, la structure hiérarchique du fichier doit être conforme au  du modèle de données d’ [expérience (XDM)](../../xdm/home.md) associé au jeu de données dans lequel il est téléchargé.

Vous trouverez des informations sur la mise en correspondance d’un fichier CSV avec une  XDM dans les [exemples de  de conversion](../../etl/transformations.md) , ainsi qu’un exemple de fichier de données JSON correctement formaté. Vous trouverez des exemples de fichiers fournis dans le  de ici :

- [CRM_..csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_..json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)